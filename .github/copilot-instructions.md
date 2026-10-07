# Repository instructions

## Project structure and architecture

This repository is a standalone browser quiz: the entire app lives in `index.html`, with no framework, server, package manager, or external runtime dependencies. Open the file directly in a browser to run it.

The HTML contains the welcome, quiz, and results views. Its inline CSS provides the layout, theme tokens, and animation; color-scheme and reduced-motion preferences are handled there. The inline JavaScript owns the question data and quiz state: `showQuestion` renders the current item, `chooseAnswer` scores and reports feedback, and `showResults` presents the final score and reaction. Keep new quiz behavior aligned with this flow rather than introducing a separate runtime or build step.

## Commands

There are no configured build, lint, or test scripts. To open the app on Windows:

```powershell
start index.html
```

There is no test suite or single-test runner. To check the inline JavaScript syntax with Node.js:

```powershell
$html = Get-Content -Raw .\index.html
[regex]::Match($html, '(?s)<script>(.*?)</script>').Groups[1].Value | node --check -
```

## Code conventions

- Keep the app self-contained in `index.html`; avoid adding dependencies or server requirements.
- Store quiz content in the `questions` array. Each question has a prompt, four answer strings, a zero-based `correct` answer index, and a short explanatory `fact`.
- Keep quiz progression in the existing state variables and functions. Update the question index and score through the quiz flow so retries and the results screen stay consistent.
- Reuse the CSS custom properties for colors and surfaces. Theme overrides belong under `prefers-color-scheme`; nonessential motion should respect `prefers-reduced-motion`.
- Preserve the existing accessible interaction patterns: native buttons, visible keyboard focus, status announcements for answer feedback, focus movement between views, and keyboard answer shortcuts.
