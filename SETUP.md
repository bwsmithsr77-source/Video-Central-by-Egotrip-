# Setup: Getting Video Central Live on GitHub Pages

Follow these steps in order. Each one builds on the last.

## 1. Create a GitHub account and repo

- Go to github.com and sign up (or log in)
- Tap the **+** in the top corner → **New repository**
- Name it `video-central`
- Leave it **Public** (required for free GitHub Pages)
- Tap **Create repository**

## 2. Upload the files

- In your new repo, tap **Add file** → **Upload files**
- Upload `index.html` and `README.md`
- Scroll down, tap **Commit changes**

## 3. Turn on GitHub Pages

- Go to **Settings** (top of the repo) → **Pages** (left sidebar)
- Under **Source**, choose **Deploy from a branch**
- Under **Branch**, choose `main` and folder `/ (root)`
- Tap **Save**

## 4. Wait for it to go live

- Give it 1–2 minutes
- Refresh the Pages settings screen — it will show:
  **"Your site is live at https://yourusername.github.io/video-central/"**
- That link is your working app

## 5. Test it for real before sharing it

- Open the live link on your phone
- Create a project, upload a real clip, run a full export end to end
- If export hangs or errors, it's almost always the ffmpeg.wasm encoder failing to download — try it on wifi, and check the log box inside the export modal for the actual error

## 6. Fill in the repo's "About" box

- On the main repo page, tap the ⚙️ gear next to **About**
- **Description:**
  > Browser-based video editor for music videos, commercial ads, and podcasts — clip trimming, audio layering, and 480p MP4 export, all client-side. No uploads, no install.
- **Website:** paste your live Pages link here
- **Topics:** add these one at a time — `video-editor` `ffmpeg-wasm` `javascript` `no-backend` `static-site` `browser-app`

## 7. Update the README with your real link

- Open `README.md` in GitHub, tap the pencil icon to edit
- Replace the placeholder line with your actual live URL
- Commit changes

## From here on: updating the app

Any time you want to change something in the app itself:
- Open `index.html` in the repo, tap the pencil icon to edit directly in GitHub, **or**
- Upload a new version of `index.html` to overwrite the old one (Add file → Upload files, same filename)

Either way, GitHub Pages automatically redeploys within a minute or two — no extra step needed.
