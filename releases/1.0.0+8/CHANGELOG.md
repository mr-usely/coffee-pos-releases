# Release 1.0.0+8

## Changes
- Test automated release workflow
- Auto-updater integration complete  
- GitHub Actions will build and release automatically
- Fixed ota_update dependency (replaced with url_launcher)

## Release Date
2026-02-05T14:58:00Z

## Technical Details
- Removed `ota_update` package (Dart SDK compatibility)
- Added `url_launcher` for APK installation
- Manual APK download with GitHub token authentication
- Improved error handling in update flow
