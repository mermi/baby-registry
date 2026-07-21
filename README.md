# 🍼 Joseph's Baby Registry

A warm, simple baby registry for welcoming **Joseph** into the world! 👶✨

Friends and family can browse gift ideas, follow helpful shopping links, and mark an item as claimed so everyone can avoid buying the same thing. Pre-loved gifts are welcome too — because tiny humans need a surprising amount of stuff! 🌱💛

## 🎁 What it does

- Organizes gift ideas into friendly, easy-to-scan sections
- Includes quantities, notes, and links to suggested products
- Lets visitors claim and unclaim available gifts
- Shows live progress for how many items have been claimed
- Includes a separate postpartum-care section for Manel 🌸
- Synchronizes claims for everyone through Firebase Firestore
- Uses anonymous sign-in so only the original visitor can undo their claim
- Looks great on both phones and larger screens 📱🖥️

## 🗂️ Project structure

```text
.
├── index.html       # Registry content, styling, and claiming logic
├── support.js      # Runtime support used by the page
├── image-slot.js   # Image-slot web component
├── assets/         # Joseph's illustration and other images
├── firestore.rules # Server-enforced claim permissions
├── firebase.json   # Firebase auth, rules, and hosting config
└── .github/        # Automatic Firebase Hosting deployment
```

There is no build step and the project has no application dependencies — the JavaScript runs directly in the browser. 🎉

## 🚀 Run it locally

Because this is a browser-based JavaScript site, it still needs to be served over HTTP for local testing. Using Node.js:

```bash
npx --yes serve . --listen 8000
```

Then visit [http://localhost:8000](http://localhost:8000).

The server is only delivering the static files; it does not run the application logic. If Node.js is unavailable, `python3 -m http.server 8000` is an equivalent convenience command, not a Python dependency of the project.

## ☁️ Deploy it

The production site is [joseph-baby-registry.web.app](https://joseph-baby-registry.web.app/). Every push to `main` automatically deploys Firebase Hosting through GitHub Actions using short-lived Google OIDC credentials; there is no stored Firebase token or service-account key.

The automated workflow deploys only these public paths:

- `index.html`
- `support.js`
- `image-slot.js`
- `assets/`

Authentication configuration and Firestore rules are intentionally excluded from automatic deployment. Release those manually after review:

```bash
npx --yes firebase-tools@15.24.0 deploy --only auth,firestore:rules
```

## 🔥 Secure shared claiming with Firebase

Claims are stored as individual documents in Firebase Firestore. Visitors sign in anonymously, so there is no login screen and no personal information is collected. Firestore Security Rules ensure that only the browser that made a claim can undo it.

This repository is connected to the `joseph-baby-registry` Firebase project. For a different environment:

1. Create a Firebase project and web app.
2. Enable **Anonymous** under Authentication → Sign-in method.
3. Create a Firestore database in production mode.
4. Add the deployed website domain under Authentication → Settings → Authorized domains.
5. Paste the Firebase web configuration into `window.REGISTRY_FIREBASE_CONFIG` in `index.html`.
6. Update the project alias in `.firebaserc`.
7. Deploy authentication, rules, and the website with `npx firebase-tools deploy --only auth,firestore:rules,hosting`.

If Firebase cannot connect, claiming is disabled instead of saving a misleading browser-only claim.

## 🧸 Making changes

Registry sections, gifts, quantities, notes, and shopping links live in the `DATA` array inside `index.html`. Update that list, refresh the page, and your changes are ready to go.

Images belong in `assets/`; update their paths in `index.html` when adding or replacing artwork.

## 💛 A little note

This registry was made to help Joseph arrive surrounded by love, useful gifts, and as few duplicate baby bathtubs as possible. Thanks for being part of his welcome party! 🎈
