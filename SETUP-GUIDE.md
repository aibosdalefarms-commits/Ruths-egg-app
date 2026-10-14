# Egg App setup guide

The app is already set up: Ruth's project is `ruths-egg-app` (database in Toronto, `northamerica-northeast2`), the config is in `index.html`, and it's live at https://ruths-egg-app.web.app. These steps are kept for reference, e.g. if the app ever needs to move to a new Firebase project.

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

1. In `index.html`, put the values from step 1.5 into `firebaseConfig`.
2. In `.firebaserc`, set the project ID.

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

- **Wrong tap?** Tap **Undo last** right away, or tap the total (✏️) and set the right number.
- **Forgot a day?** On the Record tab, use the **‹** arrow to go back to that day and tap the buttons. Sales and farm eggs for any day can be set in **Menu → History** (tap the day).
- **A hen died or was added?** Go to **Menu → Flock** and use − / +. Use the arrows to fix a past day.
- **New flock?** In **Menu → Flock**, set the new start date and the flock cost. Don't also add the flock cost in Expenses.
- **Feed from the farm?** Add it in **Expenses** as **Farm**, with what it's worth.
- **New price?** Go to **Menu → Prices**. Both phones update right away.
- **Someone else's phone?** Use **Menu → Switch user**.

## Costs

At a few dozen entries a day, the app uses a tiny fraction of Firebase's free Spark limits: 20,000 writes and 50,000 reads per day, 1 GB of storage and 10 GB of hosting transfer per month. No billing account is needed.
