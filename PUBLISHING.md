# Publisher notes

The destination is `douglasopan/ferroshift-releases`, a public repository containing distribution documentation and approved binary Release assets. The game development repository remains private and its history is not copied here.

Use the prepared publisher from the private development tools after the current artifact owner confirms the exact approved Windows/Linux file, version, size, SHA-256, platform and signing result. Never upload an owner-test Android APK, private debug artifact, source archive, credentials, saves or signing material.

Create each release as a draft, upload the approved binary and all checksum/manifest sidecars, verify GitHub's asset size and SHA-256 digest, then publish. Enable immutable releases in the repository settings before the first publication when available. Immutable releases lock assets and tags after publication; put every required file into the draft first.

The prepared naming contract pins the tag to `v<version>-<sha256 first16>` and puts the complete SHA-256 in the binary filename. Each catalogue entry points to that exact asset. Do not overwrite a release asset or use `latest/download` in the launcher.

Preserve the old Storage transport for existing launchers during migration. They have a Storage-only origin policy. Publish a compatible launcher bridge through their existing self-update path, then let new clients request `delivery: github-releases-v1`. Those clients receive a versioned GitHub URL and download the bytes directly; Firebase continues to validate accounts and return the small catalogue response.

Enable catalogue entries only after asset verification and a compare-and-swap check against the complete current manifest snapshot. Save the previous manifest for conditional rollback. Rollback restores that snapshot only if the newly activated catalogue has not changed in the meantime. Retain approved prior assets and the legacy Storage copy during the transition.

Do not publish a GitHub credential or place one in a client, README, workflow, URL or release note. Use an existing authorized publisher login through the official tool or UI. Missing publisher access is a setup gate, not permission to extract credentials from another application.

Official references: [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases), [Release assets API](https://docs.github.com/en/rest/releases/assets), [Immutable releases](https://docs.github.com/en/code-security/concepts/supply-chain-security/immutable-releases).
