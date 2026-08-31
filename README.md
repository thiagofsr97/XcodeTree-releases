# XcodeTree releases

Downloads for **XcodeTree**, a macOS menu bar app that lists the git worktrees of
the projects you point it at and opens any of them in Xcode with one click.

**[Download the latest release](https://github.com/thiagofsr97/XcodeTree-releases/releases/latest)**

This repository holds nothing but the published builds. It exists because GitHub
serves release assets from a public repository to anyone, with no account and no
token, while a private one answers an unauthenticated request as though nothing
were there. Keeping the downloads here is what lets the app update itself for
everybody; the source lives elsewhere.

## Installing

Unzip, move `XcodeTree.app` to `~/Applications`, then right-click it once and
choose **Open**. The app is ad-hoc signed rather than notarized, so Gatekeeper
asks for that confirmation the first time and never again.

From then on the app updates itself: **Check for Updates** in its menu compares
what you are running against the latest release here, shows the notes, and
installs it in place.

## Requirements

macOS 14 or later. Apple silicon and Intel are both in the same build.
