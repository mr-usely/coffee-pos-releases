# Releases Repository Setup Instructions

## ✅ What's Been Created

1. **Local Repository**: `/Users/kimju/Agent Manager Folder/coffee-pos-releases/`
   - README.md
   - latest.json (version metadata)
   - .gitignore
   - .github/workflows/release.yml (GitHub Actions)
   - releases/1.0.0+7/CHANGELOG.md

2. **Updated Flutter App**: Auto-updater now uses GitHub releases

---

## 🚀 Next Steps

### 1. Create GitHub Repository

```bash
# Navigate to releases folder
cd "/Users/kimju/Agent Manager Folder/coffee-pos-releases"

# Create repository on GitHub (via web or CLI)
# Repository name: coffee-pos-releases
# Visibility: Private

# Add remote and push
git remote add origin https://github.com/mr-usely/coffee-pos-releases.git
git branch -M main
git push -u origin main
```

### 2. Create GitHub Personal Access Token

1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Name: `coffee-pos-releases-access`
4. Expiration: No expiration (or 1 year)
5. Scopes: Select **`repo`** (Full control of private repositories)
6. Click "Generate token"
7. **COPY THE TOKEN** - you won't see it again!

### 3. Add Token to Flutter App

Edit `frontend/lib/services/update_service.dart`:

```dart
// Replace this line:
static const String _githubToken = 'YOUR_GITHUB_PERSONAL_ACCESS_TOKEN';

// With your actual token:
static const String _githubToken = 'ghp_xxxxxxxxxxxxxxxxxxxx';
```

### 4. Upload First Release APK

```bash
# Copy the APK to releases folder
cp coffee-pos-saas/frontend/build/app/outputs/flutter-apk/app-release.apk \
   coffee-pos-releases/releases/1.0.0+7/

# Commit and push
cd coffee-pos-releases
git add releases/1.0.0+7/app-release.apk
git commit -m "Add release APK for v1.0.0+7"
git push
```

### 5. Create GitHub Release

**Option A: Via GitHub Web UI**
1. Go to https://github.com/mr-usely/coffee-pos-releases/releases
2. Click "Create a new release"
3. Tag: `v1.0.0+7`
4. Title: `Release 1.0.0+7`
5. Description: Copy from `releases/1.0.0+7/CHANGELOG.md`
6. Upload: `releases/1.0.0+7/app-release.apk`
7. Click "Publish release"

**Option B: Via GitHub CLI**
```bash
gh release create v1.0.0+7 \
  --title "Release 1.0.0+7" \
  --notes-file releases/1.0.0+7/CHANGELOG.md \
  releases/1.0.0+7/app-release.apk
```

### 6. Test Auto-Updater

1. Build and install the app with the GitHub token
2. Open the app
3. The update check runs automatically on login
4. Should show "App is up to date" (since you're on 1.0.0+7)

To test update flow:
1. Increment version in `pubspec.yaml` to `1.0.0+8`
2. Build new APK
3. Upload to releases repo
4. Update `latest.json`
5. Create new GitHub release
6. Install old version (1.0.0+7) on device
7. Open app → Should prompt to update to 1.0.0+8

---

## 📝 Future Release Process

### Automated (Recommended)

1. Build APK in main repo
2. Copy to releases repo
3. Run GitHub Actions workflow (manual dispatch)
4. Workflow creates release and updates latest.json automatically

### Manual

1. Build APK: `flutter build apk --release`
2. Copy to `releases/VERSION/app-release.apk`
3. Create `releases/VERSION/CHANGELOG.md`
4. Update `latest.json` with new version
5. Commit and push
6. Create GitHub Release with tag `vVERSION`

---

## 🔒 Security Notes

- **Never commit the GitHub token to git**
- The token is embedded in the APK (obfuscated by Flutter)
- Only users with the app can download releases
- Consider rotating the token periodically
- Use environment variables for CI/CD builds

---

## 📦 Repository URLs

- **Releases Repo**: https://github.com/mr-usely/coffee-pos-releases
- **latest.json**: https://raw.githubusercontent.com/mr-usely/coffee-pos-releases/main/latest.json
- **Releases Page**: https://github.com/mr-usely/coffee-pos-releases/releases
