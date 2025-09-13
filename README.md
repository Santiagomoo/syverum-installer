Syverum Installer
=================

CLI to bootstrap new Syverum projects from the official skeleton.

Requirements
- PHP (CLI)
- Git
- Composer in PATH (`composer` or `composer.bat` on Windows)
- Node.js + npm (optional, for frontend dependencies)

Install
- Local usage: run the script directly with PHP
  - `php syverum-installer/bin/syverum new my-project`
- As a Composer binary (optional):
  - `composer global config --quiet bin-dir --absolute` (check your bin dir)
  - `composer global require syverum/installer` (when this package is published)

Usage
- Create a new project:
  - `php syverum-installer/bin/syverum new project-name`

What the installer does
- Clones `syverum-skeleton` into the target folder.
- Removes `.git` from the clone (multi‑platform) to detach from the original repo.
- Runs `composer install` for PHP dependencies (if Composer is available).
- If `package.json` exists, runs `npm install` (falls back to `yarn`/`pnpm` if available).
- Ensures the project `composer.json` has the script:
  - `composer run dev` → `php -S 127.0.0.1:3000 -t public`
- Ensures `package.json` has Tailwind scripts if missing:
  - `npm run dev` → `npx @tailwindcss/cli -i ./resources/css/app.css -o ./public/css/output.css --watch`
  - `npm run build` → same command with `--minify`

Local development
- Start the PHP dev server on port 3000:
  - `cd project-name`
  - `composer run dev`
- Start Tailwind CSS watcher in another terminal:
  - `npm run dev`
- Open `http://127.0.0.1:3000` in your browser.

Notes on Tailwind
- If your input CSS isn’t at `resources/css/app.css`, the installer tries common paths; adjust the script in `package.json` if needed.
- The installer creates `public/css/` if missing so Tailwind can write `output.css`.
- If Tailwind is not installed as a devDependency, the script uses `npx @tailwindcss/cli` which downloads and runs the official CLI.

Troubleshooting
- Composer not recognized: open a new terminal or use `composer.bat` on Windows.
- Node/npm missing: frontend install is skipped; run it later and re-run Tailwind commands.
- Port 3000 busy: change the `dev` script in `composer.json`.
