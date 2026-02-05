# Coffee POS Releases

This repository hosts APK releases for the Coffee POS SaaS mobile application.

## 📦 Latest Release

Check [`latest.json`](./latest.json) for the current version metadata.

## 🔒 Private Repository

This is a private repository. APK downloads require authentication via GitHub Personal Access Token.

## 📱 Auto-Updater

The mobile app automatically checks this repository for updates and prompts users to install new versions.

## 📂 Structure

```
releases/
├── 1.0.0+7/
│   ├── app-release.apk
│   └── CHANGELOG.md
└── 1.0.0+8/
    ├── app-release.apk
    └── CHANGELOG.md
```

## 🚀 Release Process

### Automated (GitHub Actions)

1. Push changes to main `coffee-pos-saas` repository
2. Build APK completes successfully
3. GitHub Actions workflow automatically:
   - Creates a new release
   - Uploads APK
   - Updates `latest.json`

### Manual

1. Build APK: `flutter build apk --release`
2. Create release folder: `mkdir -p releases/VERSION`
3. Copy APK: `cp build/app/outputs/flutter-apk/app-release.apk releases/VERSION/`
4. Create CHANGELOG.md in the version folder
5. Update `latest.json` with new version info
6. Commit and push changes
7. Create GitHub Release with tag `vVERSION`

## 📝 latest.json Format

```json
{
  "version": "1.0.0+7",
  "versionCode": 7,
  "downloadUrl": "https://github.com/mr-usely/coffee-pos-releases/releases/download/v1.0.0+7/app-release.apk",
  "releaseNotes": "Bug fixes and improvements",
  "releaseDate": "2026-02-05T21:26:00Z",
  "minSupportedVersion": "1.0.0+5",
  "fileSize": 80900000
}
```

## 🔐 Security

- All downloads require GitHub authentication
- APKs are signed with release keystore
- SHA256 checksums verified before installation
