# OmniProxy Model Catalog

Public distribution of the current signed model index and official recipe package.
Model weights, credentials and private signing keys are not stored here.

## Reading a snapshot

Resolve `main` to a Git commit once, then download all files at that exact commit.
Do not mix files fetched from a moving `main` branch.

- `catalog/manifest.json` describes the current compressed catalog shards.
- `catalog/manifest.ed25519` signs the exact manifest bytes.
- `catalog/*.ndjson.zst` contains the model index, hash-bound by the manifest.
- `omniproxy-recipes.json` lists the official recipe documents.
- `omniproxy-recipes.ed25519` signs the exact package bytes.
- `recipes/` contains the referenced recipe documents at the same commit.

Clients verify signatures using their embedded release public key. Recipe
documents are pinned by the Git commit; the package signature does not directly
sign their contents. Distribution does not imply model or recipe compatibility
has been tested on every device.

## Updates

An independent maintainer-run publisher validates and signs changed content,
then publishes a single commit. Unchanged content produces no new commit.
Only the current snapshot appears in the working tree. Git history records
subsequent updates; there are no date-versioned directories or `latest.json`.
Product builds, tests and client startup do not run the publisher.
