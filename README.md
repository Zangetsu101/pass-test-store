# pass-test-store

A disposable [`pass`](https://www.passwordstore.org/) password store containing dummy credentials. It is primarily a test fixture for [`android-pass-store`](../android-pass-store), including its onboarding and end-to-end test flows.

> [!WARNING]
> The private keys and passphrase in this repository are intentionally public. Never use them for real credentials or import them into a production password store.

## Test keys

Both keys can decrypt the entries in this store.

| File | Key type | Authentication subkey |
| --- | --- | --- |
| `test-key.asc` | Ed25519 primary key + Curve25519 encryption subkey | No |
| `test-key-auth.asc` | Ed25519 primary key + Curve25519 encryption subkey | Yes, Ed25519 |

The passphrase for both keys is:

```text
testpass
```

The store's `.gpg-id` is `427D2F51499FC2D6`.

## Store contents

The encrypted fixtures cover nested directories and several username formats:

```text
cards/{mastercard,visa}
dev/{github.com,gitlab.com,npmjs.com}
entertainment/{netflix.com,spotify.com}
finance/{chase.com,paypal.com,wise.com}
shopping/{amazon.com,etsy.com}
travel/{airbnb.com,uber.com}
work/{linear.app,notion.so,slack.com}
```

All credentials are fake and exist solely for testing.

## Use with android-pass-store

The app's end-to-end setup fetches these keys automatically. See [`android-pass-store/e2e/README.md`](../android-pass-store/e2e/README.md) for prerequisites, fixture details, and test commands.

Debug builds of `android-pass-store` deterministically generate a stable **SSH** key for device-key onboarding. Its public key is registered with this repository, allowing debug builds to clone it without manual key setup. This key is a test credential and must never grant access to real repositories.

When changing this repository, keep existing paths, key access, and key behavior stable unless the corresponding app tests are updated in the same change. In particular, `dev/github.com/alex.dev` is used as the onboarding readiness signal.
