---
name: openmercantil-webhook-setup
description: >-
  Register, update, rotate and delete an OpenMercantil outbound webhook so an
  account receives HMAC-signed alert and tender events instead of polling. Use
  when asked to set up event delivery, subscribe to tender or alert
  notifications, or rotate a leaked webhook signing secret.
api: OpenMercantil Webhooks API
base_url: https://openmercantil.es
auth: session cookie (ob_sess) + X-CSRF-Token — account plane, not API key
generated: '2026-08-14'
method: generated
source: openapi/openmercantil-webhooks-api-openapi.yml
operations:
  - getUserMe
  - listUserWebhooks
  - createUserWebhook
  - updateUserWebhook
  - rotateUserWebhookSecret
  - deleteUserWebhook
---

# Set up an OpenMercantil outbound webhook

This is the **account plane**, not the public read plane. An `omk_*` API
credential will not work here. You need a signed-in browser session
(`ob_sess` cookie) plus a CSRF token on every mutation.

## Step 1 — Get the CSRF token

```
GET /api/v1/user/me                              # getUserMe
```

Returns the account context and the CSRF token to send as `X-CSRF-Token` on
every mutation below. Without it you get `403` — by a wide margin the most
common failure on this plane (34 of the contract's 403 responses are CSRF).

## Step 2 — See what already exists

```
GET /api/v1/user/webhooks                        # listUserWebhooks
```

Returns `OutboundWebhook[]`: `id`, `url`, `events`, `active`, `secret_prefix`,
`key_id`, `secret_storage`, `last_success_at`, `created_at`. Note the secret
itself is **never** in this response — only the non-secret `secret_prefix`.

## Step 3 — Create

```
POST /api/v1/user/webhooks                       # createUserWebhook
X-CSRF-Token: {token}
Idempotency-Key: {your key}                      # REQUIRED
Content-Type: application/json

{"url": "https://…", "events": ["tender.matched"]}
```

Rules the schema enforces:

- `url` must match `^https://`. Plain HTTP is rejected.
- `events` must be a subset of the subscribable allowlist, max 3, unique.
  Currently subscribable: **`alert.triggered`**, **`tender.matched`**,
  **`tender.deadline`**. An empty array normalises to `alert.triggered`.
  Wildcards and unknown names fail closed.
- `Idempotency-Key` is **required**: 8–128 chars matching
  `^[A-Za-z0-9][A-Za-z0-9._:\-]{7,127}$`.

Eight event names have a defined payload contract (`borme.daily`,
`cartera.change`, `sanction.matched`, `segment.executed`, `webhook.test` in
addition to the three above), but only the three with a wired durable producer
can be subscribed. Do not offer the others as options.

## Step 4 — Capture the secret. You get one chance.

The create response is `OutboundWebhookOneTimeResponse` and contains
`webhook.secret` — 64 hex characters — with `secret_visible_once: true`. It is
**never returned again** by list or get.

The only recovery path is replaying the **identical** request with the **same**
`Idempotency-Key` inside the 24-hour window; the response carries
`idempotency_replayed: true` and `idempotency_expires_at`. After that window
the secret is unrecoverable and the only option is rotation.

So: persist the secret before doing anything else, and keep the
`Idempotency-Key` you used until you have confirmed it is stored.

A `409` means the key was reused with a **different** payload, or the window
expired. Do not retry with the same key — mint a new one.

## Step 5 — Update or deactivate

```
PATCH /api/v1/user/webhooks/{id}                 # updateUserWebhook
X-CSRF-Token: {token}

{"active": false}
```

At least one of `url`, `events` or `active` must be present. No
`Idempotency-Key` is required here because nothing secret is revealed.

## Step 6 — Rotate a compromised secret

```
POST /api/v1/user/webhooks/{id}/rotate           # rotateUserWebhookSecret
X-CSRF-Token: {token}
Idempotency-Key: {a fresh key}
```

Returns a new one-time secret and a new `key_id` under the same one-shot rules
as create. Rotate immediately if a secret was logged, pasted or committed.

## Step 7 — Delete

```
DELETE /api/v1/user/webhooks/{id}                # deleteUserWebhook
X-CSRF-Token: {token}
```

## Verifying deliveries

Deliveries are HMAC-signed; `key_id` on the webhook record identifies the
current signing key so a receiver can support rotation without downtime. Verify
the signature over the **raw received bytes**, never over a reserialised body —
the same discipline the provider applies to its own inbound Stripe callback.

Monitor `last_success_at` on the webhook record to detect a silently failing
receiver.

## One caveat

The pricing page lists webhooks under MAX as "en el roadmap · acceso anticipado
incluido", while the 1.9.3 contract already declares this full surface. If a
call returns `402`, the account's plan does not yet include the feature —
that is a plan gate, not a bug.
