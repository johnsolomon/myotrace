# Myotrace — demonstration site

Myotrace on a web page: a sign-in screen, your work saved to this repository, and a reset to
the default demonstration at any time. It runs on GitHub Pages; there is no other server.

**Simulated patients only.** This is a demonstration. Never enter real patient information.

## What is in this folder

| File | What it is |
|---|---|
| `index.html` | The app |
| `myotrace-site.json` | The site's settings: the account (stored only as a check value, never the password) and, after the first sign-in, the GitHub key, stored only encrypted |
| `data/default-workspace.json.gz` | The default demonstration: 250 simulated practice patients and one example patient. **Reset** restores it |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

After the first save, the app adds `data/workspace.enc` (your saved work, encrypted with your
password) and, after a reset, `data/workspace-before-reset.enc` (the work from before it).

## Put it online (about 10 minutes)

1. **Make a repository.** On GitHub: **+ › New repository**. Name it, for example, `myotrace`.
   Choose **Public** (GitHub Pages is free for public repositories). Create it.
2. **Upload the files.** In the new repository: **Add file › Upload files**. Drag in everything
   from this folder, including the `data` folder. On a Mac, `.nojekyll` is hidden: press
   **Cmd+Shift+.** in Finder to show it (the site works without it, but include it if you can).
   Click **Commit changes**.
3. **Turn on GitHub Pages.** **Settings › Pages**. Under *Build and deployment*: Source
   **Deploy from a branch**, branch **main**, folder **/ (root)**. Save. After a minute or two
   the page shows the site's address, such as `https://yourname.github.io/myotrace/`.
   For your own domain, enter it under **Custom domain** on the same page.
4. **Sign in** at that address with the username and password you were given.
5. **Connect saving (once).** The first sign-in asks for a GitHub key so the site can save to
   this repository:
   - On GitHub: your picture › **Settings › Developer settings › Personal access tokens ›
     Fine-grained tokens › Generate new token**.
   - **Repository access:** *Only select repositories* › this repository.
   - **Permissions › Repository permissions › Contents:** *Read and write*. Nothing else.
   - Choose an expiration, generate, copy it, and paste it into the site.

   The site checks the key, encrypts it with your password, and writes it into
   `myotrace-site.json` in the repository. The key is never kept in the browser.
6. **Change the password:** **More › Change password…** (at least 12 characters).

## Using it

- **Saving is automatic:** half a minute after each change. The chip at the top says
  *Saved*, *Unsaved changes* or *Saving…*; click it to save at once. **Save** and
  **More › Save to the server now** save too.
- **More › Reset to the default demonstration…** puts back the default. The work from just
  before is kept, and **More › Undo the last reset** brings it back.
- **More › Sign out** saves first, then clears this browser's copy.
- **When the GitHub key expires**, the chip says *Not saved*; click it and paste a new key.

## What sign-in protects, and what it does not

- Without the password, the app does not open and your saved work cannot be read: the saved
  file is encrypted with a key made from your password (AES-256-GCM, PBKDF2-SHA-256, 310,000
  rounds). The GitHub key is encrypted the same way.
- The repository is public, so the app itself and the default demonstration (simulated
  patients) can be seen by anyone who looks at the repository. Choose a long password: the
  settings file is public, so a short password could be guessed offline.
- One account. If two people are signed in at once, the last save wins.
- This is not a system for real patient data: use the app on an approved, encrypted computer
  for that, where nothing leaves the device.

## Changing the default

Set things up the way you want them, then **More › Make this the default…**. Reset then
restores that instead of the standard demonstration. (The default is stored unencrypted in
the repository; it must hold simulated patients only.)
