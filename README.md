# autobrowse-flows

Workflows that [autobrowse](https://github.com/wrenautomation/autobrowse) installs share and Wren checked.

Install one:

```sh
autobrowse workflows add <name>
```

## How a flow gets here

1. An autobrowse install compiles a flow and its proof run passes.
2. The install removes personal data on its own machine, then sends the flow to Wren.
3. Wren runs a second scrub (Presidio) and a static check: the code parses, imports only autobrowse and zod, uses no `process`, `fetch` or `eval`, and holds no literal personal values or secrets (gitleaks).
4. A person at Wren reads the code and says yes.
5. Our job opens the pull request. Nobody needs a GitHub account to share.

Each flow is in `flows/<name>/`: `index.ts`, `outline.json` and `proof.json` (step names and status only). `index.json` lists them.

Proof runs never take an irreversible step: gates are declined.

## Turn sharing off

`autobrowse share off`, `AUTOBROWSE_SHARE=off` or `DO_NOT_TRACK=1`.
