FloorMemory SDKs provide a **typed, language-native interface** to the FloorMemory APIs.

They are designed to:
- simplify authentication handling
- enforce request/response schemas
- reduce boilerplate HTTP code
- remain thin wrappers over the APIs

SDKs do not introduce custom behavior or hide API semantics.

---

## Supported SDKs

FloorMemory provides official SDKs for:

- Python
- JavaScript
- TypeScript
- Java

All SDKs are generated from the **same OpenAPI specification** and are functionally equivalent.

---


The repository contains:
- [Python SDK](https://github.com/xFloorllm/floor-memory-sdk-client/tree/main/python)
- [JavaScript SDK](https://github.com/xFloorllm/floor-memory-sdk-client/tree/main/js)
- [TypeScript SDK](https://github.com/xFloorllm/floor-memory-sdk-client/tree/main/ts)
- [Java SDK](https://github.com/xFloorllm/floor-memory-sdk-client/tree/main/java)

SDK releases track API contract versions.

---

## Build Native macOS App (npm + Electron)

This repository includes a desktop publisher UI at `scripts/floor-memory-sdk-app`.

### Prerequisites (macOS)

```bash
brew install node
```

Optional but recommended for packaging tools:

```bash
xcode-select --install
```

### Build steps

```bash
cd <repo-root>/scripts/floor-memory-sdk-app
npm ci
npm run build
npm run dist
```

What this does:
- `npm run build` builds the web UI to `web-dist/`
- `npm run dist` runs Electron Builder and creates native installers in `release/`

Expected macOS outputs:
- `release/xfloor-sdk-generation-<version>-arm64.dmg`
- `release/mac-arm64/xfloor-sdk-generation.app`

Build only macOS DMG explicitly:

```bash
npm run build
npx electron-builder --mac dmg
```

Notes:
- Current config is unsigned for macOS (`identity: null`), so Gatekeeper may warn on first launch.
- For Apple-signed/notarized distribution, code-signing credentials and notarization configuration must be added.

---

## Java JAR -> Maven Central (End-to-End)

Use this checklist when publishing the Java SDK (`dist/java`) to Maven Central.

### 1) Install required tools

macOS (Homebrew):

```bash
brew install gnupg pinentry-mac maven
```

Linux (Debian/Ubuntu):

```bash
sudo apt-get update
sudo apt-get install -y gnupg2 pinentry-curses maven curl
```

Windows:
- Install **Gpg4win** (for `gpg`)
- Install **Maven**

Quick checks:

```bash
gpg --version
mvn -version
```

### 2) Create Maven Central account + namespace

1. Sign in at `https://central.sonatype.com/`.
2. Create/verify your namespace (for example `ai.xfloor`).
3. Ensure your artifact `groupId` (for example `ai.xfloor.sdk`) belongs to that namespace.

### 3) Create Central user token (used as deploy credentials)

In Central Portal:
1. Go to account settings.
2. Create a **User Token**.
3. Copy:
- token username -> use as `--maven-central-user`
- token password -> use as `--maven-central-token`

Do not use your normal portal password for Maven deploy.

### 4) Generate GPG key (required for Maven Central signatures)

```bash
gpg --full-generate-key
```

Recommended options:
- key type: `RSA and RSA`
- key size: `4096`
- expiry: your choice (for example 2y)
- email: valid maintainer email (for example `contact@ipomo.in`)

List keys and capture the signing key id:

```bash
gpg --list-secret-keys --keyid-format LONG
```

Use the long id shown on the `sec` line as your primary signing key id.

### 5) Configure pinentry (fixes "No pinentry")

macOS:

```bash
mkdir -p ~/.gnupg
echo "pinentry-program /opt/homebrew/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf
gpgconf --kill gpg-agent
```

For this app, you can also provide passphrase non-interactively via UI/ENV (`MAVEN_GPG_PASSPHRASE`).

### 6) Publish your public key to key servers

Export public key and upload:

```bash
gpg --armor --export <PRIMARY_KEY_ID> > public-key.asc
gpg --keyserver hkps://keyserver.ubuntu.com --send-keys <PRIMARY_KEY_ID>
gpg --keyserver hkps://keys.openpgp.org --send-keys <PRIMARY_KEY_ID>
```

Verify discoverability:

```bash
gpg --keyserver hkps://keyserver.ubuntu.com --recv-keys <PRIMARY_KEY_ID>
gpg --keyserver hkps://keys.openpgp.org --recv-keys <PRIMARY_KEY_ID>
```

If Central reports missing public key, wait and retry (propagation can take time).

### 7) Validate Java POM metadata

In `dist/java/pom.xml`, ensure metadata is valid, especially:
- `<groupId>` under your verified namespace
- `<version>` new (not previously released)
- `<licenses>`, `<scm>`, `<developers>`
- valid developer email (example `contact@ipomo.in`, not `contact.in`)

### 8) Publish Java only to Maven Central using this repo script

From repo `scripts` directory:

```bash
./02-publish-sdks.sh 1.0.13 \
  --java \
  --confirm \
  --java-skip-github-publish \
  --java-publish-central \
  --mvn /abs/path/to/mvn \
  --gpg /abs/path/to/gpg \
  --maven-central-user "<CENTRAL_TOKEN_USERNAME>" \
  --maven-central-token "<CENTRAL_TOKEN_PASSWORD>" \
  --maven-central-profile-id "ai.xfloor"
```

Notes:
- By default this script requests Central auto-publish after upload.
- Add `--maven-central-no-auto-publish` only if you want manual finalization.

### 9) Check status after deploy

1. Central Portal deployment view should move from `PUBLISHING` -> `PUBLISHED`.
2. Search artifact in Central:
   - `https://central.sonatype.com/artifact/ai.xfloor.sdk/floor-memory-sdk-client`
3. Maven Central mirror (`repo1.maven.org`) can lag after portal shows `PUBLISHED`.

Direct path format:

`https://repo1.maven.org/maven2/<groupId path>/<artifactId>/<version>/`

Example:

`https://repo1.maven.org/maven2/ai/xfloor/sdk/floor-memory-sdk-client/1.0.13/`

### 10) If your GPG signing key changes (rotation process)

Use this when the old key is lost, expired, or rotated.

1. Generate a new key:

```bash
gpg --full-generate-key
```

2. Capture new key ids:

```bash
gpg --list-secret-keys --keyid-format LONG
gpg --fingerprint <NEW_KEY_ID>
```

3. Set new default signing key (`~/.gnupg/gpg.conf`):

```bash
mkdir -p ~/.gnupg
echo "default-key <NEW_KEY_ID>" >> ~/.gnupg/gpg.conf
```

4. Publish new public key to keyservers:

```bash
gpg --keyserver hkps://keyserver.ubuntu.com --send-keys <NEW_KEY_ID>
gpg --keyserver hkps://keys.openpgp.org --send-keys <NEW_KEY_ID>
```

5. Verify key can be fetched:

```bash
gpg --keyserver hkps://keyserver.ubuntu.com --recv-keys <NEW_KEY_ID>
gpg --keyserver hkps://keys.openpgp.org --recv-keys <NEW_KEY_ID>
```

6. Validate local signing with new key:

```bash
echo "maven-sign-test" | gpg --clearsign
```

7. Re-release artifact with a new version:
- Maven Central release versions are immutable.
- If any prior version was already `PUBLISHED`, bump version (`1.0.13` -> `1.0.14`) before redeploy.

8. Publish again using the Java Central command in Step 8.

### 11) Full Java release flow for new developers

From repo root:

1. Generate SDKs:

```bash
./scripts/01-generate-sdks.sh <version> --java --confirm
```

2. Publish Java artifact to Maven Central:

```bash
cd ./scripts
./02-publish-sdks.sh <version> \
  --java \
  --confirm \
  --java-skip-github-publish \
  --java-publish-central \
  --maven-central-user "<CENTRAL_TOKEN_USERNAME>" \
  --maven-central-token "<CENTRAL_TOKEN_PASSWORD>" \
  --maven-central-profile-id "ai.xfloor"
```

3. Verify:
- Central Portal deployment is `PUBLISHED`
- Central search page shows artifact
- `repo1.maven.org` path for the version is available (may take time to propagate)
