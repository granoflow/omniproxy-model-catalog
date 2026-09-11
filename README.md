# OmniProxy Model Catalog

Public distribution of the current signed model index and official recipe package.
Model weights, credentials and private signing keys are not stored here.
The repository also carries the separately signed source-neutral model-call
recipe catalog used by the model debugging and local model-call surfaces.

## Reading a snapshot

Resolve `main` to a Git commit once, then download all files at that exact commit.
Do not mix files fetched from a moving `main` branch.

- `catalog/manifest.json` describes the current compressed catalog shards.
- `catalog/manifest.ed25519` signs the exact manifest bytes.
- `catalog/*.ndjson.zst` contains the model index, hash-bound by the manifest.
- `omniproxy-recipes.json` lists the official recipe documents.
- `omniproxy-recipes.ed25519` signs the exact package bytes.
- `recipes/` contains the referenced recipe documents at the same commit.
- `model-call-test-recipes.json` contains release-owned remote debug recipes
  and common local model-call recipes.
- `model-call-test-recipes.ed25519` signs the exact model-call catalog bytes.
- `generated-model-call-test-recipes.json` contains the generated long-tail
  model-call recipes bound to fixed Hub revisions.
- `generated-model-call-test-recipes.ed25519` signs the generated catalog bytes.

Clients verify signatures using their embedded release public key. Recipe
documents are pinned by the Git commit; the package signature does not directly
sign their contents. The model-call catalog is a separate schema and signature;
the generated catalog has its own schema and signature. Their presence does not
imply model or recipe compatibility has been tested on every device.

## Updates

An independent maintainer-run publisher validates and signs changed content,
then publishes a single commit. Unchanged content produces no new commit.
Only the current snapshot appears in the working tree. Git history records
subsequent updates; there are no date-versioned directories or `latest.json`.
Product builds, tests and client startup do not run the publisher.
