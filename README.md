# Luzzes — GitHub Pages bundle

This folder is the whole site. Three files and a folder marker:

| file | why it exists |
| --- | --- |
| `index.html` | the entire application — one self-contained file, no build step, no network calls |
| `.nojekyll` | empty marker that tells GitHub Pages to skip Jekyll and serve these files exactly as they are |
| `404.html` | a 404 that sends visitors back to the workspace instead of GitHub's default page |
| `README.md` | this file (it is published too, which is fine) |

## Publish it (5 steps)

1. Create a repository (public, or private on a plan that includes Pages).
2. **Add file → Upload files**, then drag in `index.html`, `.nojekyll`, `404.html` and `README.md`.
   Drag the *contents* of this folder, not the folder itself — the files must sit at the repository root.
3. Commit the change.
4. **Settings → Pages → Build and deployment → Source: Deploy from a branch**, then **Branch: main**, **Folder: / (root)**, and **Save**.
5. Wait ~1 minute. The site appears at `https://<your-username>.github.io/<repo-name>/`.

If you would rather have it at `https://<your-username>.github.io/` with no repo path,
name the repository `<your-username>.github.io` and put the same files at its root.

## Notes worth knowing

- **Uploading the `.zip` to GitHub will not work.** GitHub's web interface stores binaries as-is;
  it never unpacks them. Either extract on your machine first (see below) or unpack inside a
  Codespace, which does have a real shell.
- **Model endpoints are the one thing a static host limits.** Demo mode works everywhere with no
  setup. "Local model" mode needs CORS enabled on your model server and, because Pages is HTTPS,
  the browser will usually refuse a plain-`http://localhost` request (mixed content /
  Private Network Access). "Connected model" mode needs a provider that sends CORS headers —
  most hosted APIs do not, because they expect a server to hold the key. The app reports the
  real error in those cases instead of pretending the request succeeded.
- **Projects are stored per origin** in your browser's IndexedDB. Building at
  `https://you.github.io/luzzes/` keeps your projects under that URL. Moving to a custom domain
  later means exporting from Settings → Storage (`.zip` or `.json`) and importing on the new origin.
- **Updating the site:** upload a new `index.html` over the old one. Pages caches for a few
  minutes, so a hard refresh may be needed to see the change.
- Nothing here needs a build tool, a Node install, or a CI workflow.

## Extract this zip on your machine

- **Windows:** right-click the zip → *Extract All…* → pick a folder → *Extract*.
- **macOS:** double-click the zip; Finder creates a folder beside it.
- **Linux / any shell:** `unzip luzzes-github-pages.zip -d luzzes-pages`

On macOS and Linux the `.nojekyll` file starts with a dot, so it is hidden. In Finder press
`Cmd + Shift + .` to show hidden files before dragging. If `.nojekyll` refuses to upload,
leave it out — this site has no underscore-prefixed paths, so Jekyll has nothing to skip.
