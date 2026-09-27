# dsh-plugin-mode-conduct

Mode-aware runtime conduct and standing lessons for DeepSeek Harness (DSH) sessions.
Windows, Node 20+, no dependencies.

A DSH *bundle*: installing it adds one row to a profile and contributes two runtime-context
statements to every session in that profile.

| Statement | When it appears |
| --- | --- |
| `conduct:full-access` | Only while the session's file policy is `danger-full-access` |
| `lessons:harness` | Every session, every mode |

## Install

```powershell
# from npm, into a profile (this is the whole install)
dsh plugin --profile web add dsh-plugin-mode-conduct
```

Or from a checkout, without npm:

```powershell
dsh plugin --profile web add file:D:/path/to/dsh-plugin-mode-conduct
```

The Web GUI offers the same thing: sidebar **Plugins → install**, then switch the row on.
Either way the row lands in the profile's `cordis.patch.yml`; the profile's own
`package.json` gains the dependency.

Verify it is live: open a new session and look for the two statements in the runtime context,
or run the unit tests from a checkout:

```powershell
node test/unit.mjs
node test/integration.mjs
```

## Configure

Patch the row the bundle inserts:

```yaml
- id: mode-conduct
  config:
    enabled: true
    content: digest          # digest | full — how much of the full-access conduct is injected
    lessonsEnabled: true
    lessonsFile: 'D:\dsh\AGENTS.md'
    lessonsMaxBytes: 65536
```

Unknown keys are refused by design: the plugin validates its config against the composed row and
**disables itself with a loud log line** rather than letting a config mistake take the host down.

## Uninstall

```powershell
dsh plugin --profile web remove dsh-plugin-mode-conduct
```

Or disable it without uninstalling:

```yaml
- id: mode-conduct
  enabled: false
```

## Licence

MIT
