# TrueCollector — releases

This repository holds **only what an update needs**: the installers for
TrueCollector, the Editor and the Launcher, the sha256 digest of every one of
them, the schema version each release speaks, and the notes. There is no source
code here, and there never will be — the source lives in a private repository
this one does not point at.

## Why it is separate

The Launcher checks for updates by asking GitHub's API for this repository's
release list. While it asked the private source repository instead, GitHub
answered `404` to anyone not signed in — which it does on purpose, so that a
stranger cannot tell a private repository from one that does not exist. The
result was an update mechanism that worked for exactly one person: whoever had
a token in their environment.

Moving the releases here fixes that without publishing the source. What becomes
readable is what anyone installing an update receives anyway.

## The installers are not signed

Windows will warn you when you run one. That is expected, and the warning text
is announced in each release's own notes **before** you see it — if what Windows
shows you does not match what the notes said, something is wrong and you should
stop.

## Verifying what you downloaded

Every release publishes `checksums.json`, listing one sha256 per asset. On
Windows:

```powershell
Get-FileHash .\TrueCollector_0.1.2_x64-setup.exe -Algorithm SHA256
```

Compare it with the entry for that file name. The Launcher does this for you and
refuses an installer whose digest does not match, without offering a way past
the refusal.

## `schema.json`

A release declares which pack schema version its builds speak. That is how the
Launcher can tell you, **before** you install anything, which of your packs
would stop opening afterwards — by name, not as a count.
