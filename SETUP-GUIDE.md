# Egg App setup guide

## 1. Ruth creates the Firebase project (about 5 minutes)

Signed in with Ruth's Google account at https://console.firebase.google.com:

1. **Create a project** and name it e.g. `egg-app`. Google Analytics isn't needed, so turn it off. It stays on the free **Spark** plan.
2. **Build → Firestore Database → Create database**
   - Location: **`northamerica-northeast2` (Toronto)**. This can't be changed later.
   - Start in **production mode**. The real rules get deployed in step 3.
3. **Build → Authentication → Get started → Sign-in method → Anonymous → Enable → Save**
4. **⚙ Project settings → Users and permissions → Add member**: Nate's Google email, role **Owner**. This lets Nate deploy from his computer while the project and all its data stay under Ruth's account.
5. **⚙ Project settings → General → Your apps → Web (`</>`)**
   - App nickname: `Egg App`. **Don't** tick "Also set up Firebase Hosting" here.
   - Copy the `firebaseConfig` values it shows.

## 2. Connect the app to the project

1. In `index.html`, replace the `REPLACE_ME` values in `firebaseConfig` with the values from step 1.5.
2. In `.firebaserc`, replace `REPLACE_ME` with the project ID.

## 3. Deploy

From the Egg App folder, signed in to the Firebase CLI as Nate:

```bash
firebase deploy
```

This publishes the database rules and the app. The address will be `https://<project-id>.web.app`.

## 4. Install on each phone (Android)

1. Open the address in **Chrome**.
2. Tap **⋮ → Add to Home screen → Install**.
3. Open **Egg App** from the home screen and tap your name.

## Everyday notes

- **Wrong tap?** Tap **Undo last** right away, or fix it in **Menu → History**.
- **Forgot a day?** Go to **Menu → History → Add** and pick the date.
- **New price?** Go to **Menu → Prices**. Both phones update right away.
- **Someone else's phone?** Use **Menu → Switch user**.

## Costs

At a few dozen entries a day, the app uses a tiny fraction of Firebase's free Spark limits: 20,000 writes and 50,000 reads per day, 1 GB of storage and 10 GB of hosting transfer per month. No billing account is needed.
