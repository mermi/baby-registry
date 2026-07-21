# 🍼 Joseph's Baby Registry

A warm, simple baby registry for welcoming **Joseph** into the world! 👶✨

Friends and family can browse gift ideas, follow helpful shopping links, and mark an item as claimed so everyone can avoid buying the same thing. Pre-loved gifts are welcome too — because tiny humans need a surprising amount of stuff! 🌱💛

## 🎁 What it does

- Organizes gift ideas into friendly, easy-to-scan sections
- Includes quantities, notes, and links to suggested products
- Lets visitors claim and unclaim available gifts
- Shows live progress for how many items have been claimed
- Includes a separate postpartum-care section for Manel 🌸
- Works without a backend by saving claims in the visitor's browser
- Can optionally sync claims for everyone through Firebase Firestore
- Looks great on both phones and larger screens 📱🖥️

## 🗂️ Project structure

```text
.
├── index.html       # Registry content, styling, and claiming logic
├── support.js      # Runtime support used by the page
├── image-slot.js   # Image-slot web component
└── assets/         # Joseph's illustration and other images
```

There is no build step and no package installation required — it is a small, static website. 🎉

## 🚀 Run it locally

Start any static file server from the repository root. For example, with Python:

```bash
python3 -m http.server 8000
```

Then visit [http://localhost:8000](http://localhost:8000).

## ☁️ Deploy it

Serve the repository root with any static hosting provider, such as GitHub Pages, Netlify, Vercel, or Firebase Hosting. The site only needs these paths:

- `index.html`
- `support.js`
- `image-slot.js`
- `assets/`

## 🔥 Optional shared claiming with Firebase

By default, claimed gifts are stored in each visitor's browser using `localStorage`. That is handy for previews, but claims will not be shared between different people or devices.

To synchronize claims for everyone, create a Firebase project with Firestore and add its web configuration to `window.REGISTRY_FIREBASE_CONFIG` near the top of `index.html`. When no valid Firebase project is configured, the registry automatically falls back to browser-only storage.

> 💡 Remember to configure appropriate Firestore security rules before making the registry public.

## 🧸 Making changes

Registry sections, gifts, quantities, notes, and shopping links live in the `DATA` array inside `index.html`. Update that list, refresh the page, and your changes are ready to go.

Images belong in `assets/`; update their paths in `index.html` when adding or replacing artwork.

## 💛 A little note

This registry was made to help Joseph arrive surrounded by love, useful gifts, and as few duplicate baby bathtubs as possible. Thanks for being part of his welcome party! 🎈
