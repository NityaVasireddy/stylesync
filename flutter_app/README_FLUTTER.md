# StyleSync AI — Flutter conversion

This package replaces the original React/Vite client with a Flutter mobile app while retaining the existing Node.js/Express API, its AI/outfit logic, auth, validation, and storage. Server-side JavaScript cannot be converted into Flutter client code without changing the architecture, so it remains in `backend/` and is called by the Flutter app.

## Requirements
- Flutter SDK (stable), Dart SDK bundled with Flutter
- Node.js 18+ for the API

## Run the backend
```bash
cd backend
npm install
# configure backend/.env using the supplied .env.example (copy it to .env)
npm start
```
The backend listens on port 5000 by default. Ensure it is reachable from the device.

## Run Flutter
```bash
cd flutter_app
# Generate Android/iOS runner folders once if they are not present in this package
flutter create --platforms=android,ios .
flutter pub get
flutter analyze
flutter run
```

### API URL notes
- Android emulator: default is `http://10.0.2.2:5000/api`.
- iOS simulator: use `http://127.0.0.1:5000/api`.
- Physical phone: use `http://YOUR_COMPUTER_LAN_IP:5000/api` and ensure both devices share a network. Enter the URL on the sign-in screen under **Server connection settings**. Include `/api`.
- For a deployed HTTPS API, use `--dart-define=API_BASE_URL=https://your-api.example.com/api`.

The app supports registration/login, persistent JWT session, wardrobe retrieval, image capture/gallery upload, backend garment tagging, occasion-based outfit suggestions, wardrobe insights, and sign out. AI results depend on backend configuration and provider keys; no claim is made that external AI is available without configuration.

## Notes
- Android camera/gallery permissions are managed by `image_picker`; if testing on iOS, add the required camera and photo-library usage descriptions to `ios/Runner/Info.plist`.
- The original dataset images are included under `flutter_app/assets/dataset/` for future use in UI cards. Live wardrobe images are currently displayed as garment metadata tiles; uploaded images are sent to the API.
- I could not execute `flutter analyze` or build the APK in this environment because the Flutter SDK is not available here. Run the commands above locally and share any output if a platform-specific issue appears.
