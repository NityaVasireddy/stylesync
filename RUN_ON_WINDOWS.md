# Run StyleSync AI on Windows

## 1. Requirements
- Node.js 18 or newer
- Flutter stable SDK (for the Flutter app)
- Android Studio with an Android emulator, or a physical Android phone

Check installation in PowerShell:
```powershell
node --version
npm --version
flutter --version
flutter doctor
```

## 2. Start the backend
Open PowerShell in the project folder:
```powershell
cd backend
Copy-Item .env.example .env
npm install
npm test
npm start
```
Leave this terminal running. Open `http://localhost:5000/api/health` in a browser; a JSON response with `"status":"ok"` means the API is running.

The supplied `.env.example` uses local JSON storage and mock AI by default. This lets the demo run without Supabase or an AI API key. Do not commit `.env`.

## 3. Start the Flutter app
Open a second PowerShell window:
```powershell
cd flutter_app
flutter create --platforms=android,ios,windows .
flutter pub get
flutter analyze
flutter run
```
If Flutter asks which device to use, choose your Android emulator or Windows desktop.

API base URL depends on where the app runs:
- Android emulator: `http://10.0.2.2:5000/api`
- Windows desktop: `http://127.0.0.1:5000/api`
- iOS simulator: `http://127.0.0.1:5000/api`
- Physical phone: `http://YOUR_COMPUTER_LAN_IP:5000/api` (phone and computer must share Wi-Fi)

On the sign-in screen, expand **Server connection settings** and enter the matching URL. Include `/api`.

## 4. Push to GitHub
Run these from the `StyleSync_Flutter` project root (the folder containing this README and `.gitignore`):
```powershell
git init
git add .
git status
git commit -m "Prepare StyleSync Flutter app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```
Replace the remote URL with your actual GitHub repository URL. If `git remote add origin` says the remote already exists, use `git remote set-url origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git` instead.

Before pushing, check `git status` and make sure `.env`, `backend/db.json`, and `node_modules` are not staged. The `.gitignore` excludes them.
