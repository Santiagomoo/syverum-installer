Syverum Installer
=================

CLI to bootstrap new Syverum projects from the official skeleton.

Requirements
- PHP (CLI)
- Git
- Composer in PATH (`composer` or `composer.bat` on Windows)
- Node.js + npm (optional, for frontend dependencies)

Install
  - `composer global require syverum/installer`

Usage
- Create a new project:
  - `syverum new project-name`

What the installer does
- Runs `composer install` for PHP dependencies
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

Troubleshooting
- Composer not recognized: open a new terminal or use `composer.bat` on Windows.
- Node/npm missing: frontend install is skipped; run it later and re-run Tailwind commands.
- Port 3000 busy: change the `dev` script in `composer.json`.
