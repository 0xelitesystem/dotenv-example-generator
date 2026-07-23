# dotenv Example Generator

Paste a real .env file and get a sanitized .env.example with secret values stripped and comments kept, ready to commit, all in your browser.

## Live demo

https://0xelitesystem.github.io/dotenv-example-generator/

## Features

- Live output: the sanitized .env.example updates as you type
- Faithful parsing: comments and blank lines are preserved exactly, `export KEY=value` works, single and double quoted values work, inline comments after values are kept, and a `#` inside quotes stays part of the value
- Values containing `=` signs are handled correctly (only the first `=` splits key from value)
- Lines that do not parse pass through unchanged and are flagged in a notices area
- Three placeholder styles: empty value (`KEY=`), `your-value-here`, or a hint comment derived from the key name (for example `DATABASE_URL= # your database connection string`)
- Optional, clearly labeled setting to keep values that look non-secret (booleans, plain numbers, localhost URLs without credentials), off by default
- Secret detection notice: counts values that look like live credentials (high-entropy strings, URLs with `user:pass@`) and tells you how many were stripped
- Copy button and a Download .env.example button, both fully local
- A .gitignore reminder box with the exact lines to add and why
- Load example button with an obviously fake sample .env
- Dark theme by default with a light mode toggle that persists
- Single HTML file, no external dependencies, works offline

## How it works

The tool splits your input into lines and parses each one in memory. Comment lines and blank lines are copied through untouched. For every `KEY=value` pair, the value is replaced with the placeholder style you picked while the key, any `export` prefix, quoting style, and inline comments are kept. A small heuristic (entropy, length, credential-shaped URLs) counts how many of the stripped values looked like real live secrets so you know what to rotate. Anything the parser cannot understand is passed through unchanged and listed as a warning, so the output never silently loses a line.

**Positioning note:** this tool sanitizes an env file so you can share it. It is a sibling of [env-var-checker](https://github.com/0xelitesystem/env-var-checker), which validates that every required variable is present. One checks, one scrubs, and they pair well: generate the .env.example here, then use env-var-checker to verify a teammate's real .env against it.

## Privacy

Everything runs in your browser. The page makes zero network requests: nothing you paste is uploaded, stored, or sent anywhere, which is the whole point of a tool you paste real credentials into. You can disconnect from the internet and it keeps working.

## License

MIT
