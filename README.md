# copilot-chat student plan workaround

MicroSlop probably changed something in the backend yesterday night - It dosen't work anymore

GitHub [removed Claude Sonnet and Opus from the Student Plan on March 12, 2026](https://github.com/orgs/community/discussions/189268) to keep Copilot "free and accessible." This repo builds the extension from source with a setting that lets you pick your preferred Claude model when it's available in your token.

---

## requirements

- Node.js 20+
- VS Code
- GitHub Copilot access (student plan works)

---

## build and install

Clone the repo and install deps, then:

```bash
# build (needs extra heap or it OOMs)
NODE_OPTIONS="--max-old-space-size=8192" node .esbuild.ts --sourcemaps

# package
./node_modules/.bin/vsce package --no-dependencies

# install (force-replaces any existing marketplace version)
code --install-extension copilot-chat-0.39.1.vsix --force
```
(you can also just install it with that line since it's already built)

Then run `Developer: Reload Window` from the command palette.

---

## configure

Add this to your `settings.json` (`Preferences: Open Settings (JSON)`):

```json
"github.copilot.chat.autoMode.preferredModel": "claude-sonnet-4.6"
```

valid values: `"default"` | `"claude-sonnet-4.6"` | `"claude-opus-4.6"`

If the model isn't available in your session, Auto falls back to its normal selection.

---

## notes

- The setting is in the `preview` group and may not appear in the Settings UI search. Just put it in `settings.json` directly.
- If VS Code loads the marketplace version instead of this one, check the Extensions panel — source should say `VSIX` and version should be `0.39.1`.
