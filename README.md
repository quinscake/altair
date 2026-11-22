# Altair

Gym, protein and vitamin tracker. *Ready when the call comes.*

The whole app is one file, `index.html`. Your data does not live in this repo. It lives in a separate **private** repo as `data.json`, and the app commits to it every time you log something.

## Setup (about 5 minutes)

### 1. Private data repo
1. Create a new repository named `altair-data` and set it to **Private**.
2. Tick **Add a README file** so the `main` branch exists.
3. Leave it otherwise empty. Altair creates `data.json` on its first sync.

### 2. App repo (this one)
1. Create a repository named `altair` and upload all of these files together (drag them in at once):
   `index.html`, `manifest.json`, `apple-touch-icon.png`, `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `README.md`
2. Go to **Settings → Pages**. Under Source, choose **Deploy from a branch**, then pick `main` and `/ (root)`, and save.
3. After a minute the app is live at `https://<your-username>.github.io/altair/`.

GitHub Pages on a free account needs this repo to be **public**. That's fine, because it only holds code. To keep the code private too, you need GitHub Pro.

### 3. Access token
1. Open https://github.com/settings/personal-access-tokens/new
2. Name it `altair` and pick an expiry (a year is fine).
3. Under **Repository access**, choose **Only select repositories → altair-data**.
4. Under **Permissions → Repository permissions**, set **Contents: Read and write**. Nothing else is needed.
5. Generate the token and copy it (it starts with `github_pat_`).

### 4. Connect
1. Open your Pages URL.
2. Tap **Parameters** (top right), then **GitHub sync → Configure**.
3. Fill in:
   - **Data repository:** `<your-username>/altair-data`
   - **Branch:** `main`
   - **File:** `data.json`
   - **Access token:** the token from step 3
4. Tap **Save and sync**. The status should read **Saved to GitHub**.

Repeat step 4 on each phone or laptop. Every device then reads and writes the same `data.json`.

## Home screen (iPhone)
1. Open your Pages URL in Safari, tap **Share → Add to Home Screen**. It gets the yellow star icon and opens full screen with no browser bars.
2. If you added it before the icons existed, delete the old "A" icon first, then add it again. iPhone saves the icon only when you add it.
3. Set up **GitHub sync inside the home-screen app**. On iPhone it keeps its own storage, separate from Safari, so a token saved in Safari won't carry over.

## Moving your data from the Claude version
1. In the Claude-hosted Altair, open **Parameters → GitHub sync → Copy my data**.
2. In your Pages copy, open the same dialog, tap **Paste data from another device**, paste, and tap **Import**.

If copying is blocked there, use the Pages copy from the start. Nothing has been logged yet beyond today.

## How sync works
- Changes are batched and committed about 2.5 seconds after your last tap. Commit messages look like `altair: update 2026-11-22 18:40`.
- The app pulls the latest file when it opens and whenever you switch back to the tab.
- If another device committed first, Altair refreshes and retries, so nothing is overwritten blindly.
- The token is stored only in that browser's local storage. **Disconnect** removes it. The data stays in the repo.
- Your full history is the commit log of `altair-data`. To undo a bad day, restore an older `data.json` from there.

## Troubleshooting
| Message | Fix |
|---|---|
| Token rejected | The token expired or was mistyped. Make a new one. |
| No access | The token is missing **Contents: Read and write**, or `altair-data` wasn't selected. |
| Repository, branch or file path not found | Check the spelling of `owner/name`, and confirm the repo has a `main` branch (step 1.2). |
| Can't reach GitHub from here | You're in the Claude-hosted copy, which can't call GitHub. Use your Pages URL. |
