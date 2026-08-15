# Tailwind CSS v4 — Crash Course Codes

Lecture codes for my Tailwind CSS v4 crash course.

Every lecture is a **separate folder**. Each one is finished and works alone.
You can copy only the folder you need. No setup for the whole repo.

## How to run a lecture

Pick one lecture folder, then:

```bash
cd section-1/lecture-3
npm install
npm run watch
```

Now open `index.html` in your browser.

`npm run watch` keeps running. When you edit `index.html`, the CSS is rebuilt
automatically. Just refresh the browser.

If you only want to build one time:

```bash
npm run build
```

> Stop `watch` with `Ctrl + C`.

## Lectures

| Folder | What is inside |
| --- | --- |
| `section-1/lecture-1` | No codes (theory only) |
| `section-1/lecture-2` | No codes (theory only) |
| `section-1/lecture-3` | First setup — Tailwind CLI, `input.css`, first classes |
| `section-1/lecture-4` | Text color classes |
| `section-2/lecture-1` | Small UI — card, input, list, button |
| `section-2/lecture-2` | No codes (theory only) |

Folders with `# No Codes` in the README are talking lectures. Nothing to run.

## What is inside a code lecture

```
lecture-3/
├── index.html          <- your HTML, write classes here
├── package.json        <- build / watch scripts
├── src/input.css       <- Tailwind config (v4 style)
└── output/output.css   <- generated, do not edit
```

`output/output.css` is **not** in this repo. It is created when you run
`npm run build` or `npm run watch`. This is normal.

## About Tailwind v4

Tailwind v4 has **no `tailwind.config.js`**. Config now lives in CSS:

```css
@import "tailwindcss" source(none);

@source "../index.html";
```

- `source(none)` — turn off automatic file scanning.
- `@source` — tell Tailwind which files to read classes from.

So if you add a new HTML file, add one more `@source` line for it.
If you forget, your new classes will not appear in the CSS.

## Requirements

- Node.js (v20 or newer is fine)
- A browser
- VS Code extension **Tailwind CSS IntelliSense** (optional, but helpful)

## Tips for students

- Copy one lecture folder into your own project folder and play with it.
- Do not delete `src/input.css`. It is small, but it is the config.
- Class not working? First check `npm run watch` is still running.
- Still not working? Check the class name spelling, then hard refresh the browser.

Happy coding 🎉
