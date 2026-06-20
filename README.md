# 🚀 Mini Jenkins Freestyle Pipeline — Practice Repo

A compact, beginner-friendly playground for practicing Jenkins Freestyle Pipeline jobs. Clean, visual guidance for creating, testing, and publishing build artifacts with Jenkins — without a license section.

---

## 🌟 Overview
This repo contains a minimal sample project and step-by-step instructions to practice Jenkins Freestyle jobs: Git SCM, build steps, artifacts, test reports, and basic notifications.

## 📁 Repo layout
- src/ — sample scripts or tiny app
- build/ — generated artifacts (gitignored)
- jenkins/ — optional job snippets or templates
- redd.md — this file (visual README)

## ⚙️ Prerequisites
- Jenkins (LTS recommended)
- Git access to this repo
- Node / Python / or other runtime depending on samples
- Optional: Docker for containerized builds

## 🚦 Quickstart — Create the Freestyle Job
1. Jenkins → New Item → name → Choose "Freestyle project".
2. Source Code Management → Git: paste repo URL and credentials if private.
3. Build Triggers → choose Poll SCM or webhook.
4. Build → Add "Execute shell" (Unix) or "Execute Windows batch command" (Windows). Paste example steps below.
5. Post-build Actions → Archive artifacts (e.g., `build/**/*`) and publish test reports if any.

## 🛠 Example build steps

Unix shell (Execute shell):

```bash
#!/usr/bin/env bash
set -euo pipefail
echo "=== Install dependencies ==="
if [ -f package.json ]; then
  npm ci
fi

echo "=== Run tests ==="
npm test || true

echo "=== Build artifact ==="
mkdir -p build
echo "mini-jenkins-$(date +%Y%m%d%H%M%S)" > build/release.txt
tar -czf build/release.tar.gz build/
```

Windows batch (Execute Windows batch command):

```bat
@echo off
echo === Build ===
if exist package.json (
  npm ci
)
mkdir build 2>nul
echo mini-jenkins-%date%-%time%> build\release.txt
powershell -Command "Compress-Archive -Path build\* -DestinationPath build\release.zip"
```

## 📦 Artifacts & test reports
- Archive artifacts: `build/**/*`
- Publish JUnit: `test-results/**/*.xml`

## 🔎 Troubleshooting
- "command not found": ensure tools are on the Jenkins node PATH.
- Permissions: verify the Jenkins user can write the workspace.
- Tests failing on CI: compare environment, node versions, and env vars.
- Artifacts not archived: confirm files are created in the workspace and match archive globs.

## ✨ Job style tips (visual & readable)
- Name steps descriptively.
- Use console echoes like `=== Step ===` to make logs scannable.
- Keep build steps idempotent and fast.

## 🤝 Contributing
1. Fork the repo
2. Create a branch: `git checkout -b fix/jenkins-docs`
3. Edit and test locally
4. Open a PR describing changes

## 📬 Contact
Questions or suggestions? Open an issue in this repo.

---
