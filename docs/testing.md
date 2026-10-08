# Testing with the private test copy

The test copy runs entirely on this computer using Firebase's emulators. Nothing touches the real database, and everything in it is wiped when it stops.

## Start it

You need Java 21 (Eclipse Temurin) and the Firebase CLI. Run each command in its own terminal from the Egg App folder.

```powershell
$env:PATH = "C:\Program Files\Eclipse Adoptium\jdk-21.0.12.101-hotspot\bin;" + $env:PATH
firebase emulators:start --only "auth,firestore" --project demo-egg-app
```

```powershell
node tools/serve.js 5080
```

Then open http://localhost:5080. When the app is opened at `localhost`, it connects to the emulators automatically, using the `demo-egg-app` project on ports 9098 and 8081. See the "Testing on this computer only" block in `index.html`. On the real website that code never runs.

The emulator ports differ from Bosdale Receipts (9099/8080), so both test copies can run at the same time.

The real security rules (`firestore.rules`) are loaded into the emulator, so tests exercise the same rules as the live app.

## Wipe the test data without restarting

```bash
curl -X DELETE "http://127.0.0.1:8081/emulator/v1/projects/demo-egg-app/databases/(default)/documents"
```
