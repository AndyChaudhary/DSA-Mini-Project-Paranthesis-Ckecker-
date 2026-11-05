# DSA-Mini-Project-Paranthesis-Ckecker-
Balanced Parentheses & Syntax Checker

A college DSA project that validates brackets `() [] {}` and HTML/XML tags using the **Stack** data structure (LIFO), with line/column error reporting and an animated push/pop visualizer.

**Tech:** HTML5, CSS3, vanilla JavaScript. No backend, no APIs, no build step.

## Run it
- **Locally:** double-click `index.html`, or run `python3 -m http.server` in this folder and open `http://localhost:8000`.
- **Replit:** create a new Repl with the *HTML, CSS, JS* template, replace its files with these four, and press **Run**.

## Files
| File | Purpose |
|---|---|
| `index.html` | Page structure and the six sections |
| `style.css` | Dark theme, responsive layout, animations |
| `script.js` | Stack class, validators, UI logic |
| `README.md` | This document |

## Algorithm
```
1. Create an empty stack
2. Traverse the input character by character
3. Opening bracket → push
4. Closing bracket:
     stack empty → "unexpected closing bracket"
     else pop the top and compare types
5. Types differ → report the first mismatch
6. End of input and stack not empty → "unclosed opening bracket"
7. Stack empty and no error → balanced
```
For HTML, the stack holds tag names. `<div>` is pushed; `</div>` must match the top. Comments, void tags (`img, br, hr, input, meta…`) and self-closing tags (`<x />`) are never pushed.

## Complexity
- **Time: O(n)**: one pass, and push/pop/peek are O(1).
- **Space: O(n)**: worst case every character is an opening bracket.

## Important functions (`script.js`)
| Function | What it does |
|---|---|
| `class Stack` | The stack ADT: `push`, `pop`, `peek`, `isEmpty`, `snapshot` |
| `validateBrackets(text, skip)` | Scans once, pushes openers, pops on closers, tracks line/column while scanning. `skip` ignores strings and comments |
| `validateTags(text)` | Regex finds each tag; pushes openers, pops on matching closers, distinguishes *incorrectly nested* from *mismatched* |
| `finish(stack, steps, type)` | After the scan: empty stack means balanced, otherwise reports the unclosed opener |
| `fail(steps, stack, error)` | Builds the error result and records the failing step |
| `posAt(text, index)` | Converts a character index to line and column |
| `run(text, mode, skip)` | Entry point; handles empty input safely |
| `showResult`, `validate` | Render the green/red result card and highlight the error in the editor |
| `loadViz`, `stepViz`, `playViz` | Drive the animated stack: each validator returns a `steps` list that the visualizer replays |
| `runAllTests` | Runs every test case and compares actual against expected |
