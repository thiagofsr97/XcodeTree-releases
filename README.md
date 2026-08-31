# XcodeTree

A macOS menu bar app that lists the git worktrees of the projects you point it
at, and opens any of them in Xcode, or whichever editor you prefer, with one
click.

Xcode has no worktree awareness. Every worktree of the same repository produces
an identically named `.xcodeproj`, so "Open Recent" becomes a list of
indistinguishable entries and switching means digging through a file picker. This
replaces that with a menu, and cleans up after a worktree when you are done with
it.

**[Download the latest release](https://github.com/thiagofsr97/XcodeTree-releases/releases/latest)**

This repository holds nothing but published builds. It is public so that the app
can update itself for anyone, with no GitHub account and no token: GitHub serves
a public repository's releases to all comers, and answers a request for a private
one as though nothing were there. The source lives elsewhere.

## Requirements

macOS 14 or later. Apple silicon and Intel are both in the same build.

Xcode is only needed if the repositories you point it at are Xcode projects; the
simulator and derived-data features appear only for those. `gh` is optional, and
without it the pull request column stays empty.

## Installing

1. Download the zip from the [latest release](https://github.com/thiagofsr97/XcodeTree-releases/releases/latest)
   and unzip it.
2. Move `XcodeTree.app` to `~/Applications` or `/Applications`.
3. **Right-click it and choose Open**, then confirm. Do not double-click it the
   first time.

Step 3 matters. The app is ad-hoc signed rather than notarized, so Gatekeeper
refuses a plain double-click and offers no way past it. Opening from the
right-click menu gives you the "open anyway" choice, once, and never asks again.

If macOS insists the app is damaged, the quarantine flag survived the move.
Clear it and open normally:

```sh
xattr -dr com.apple.quarantine ~/Applications/XcodeTree.app
```

## First run

There is no Dock icon and no window. XcodeTree is the small branch glyph in the
menu bar, and everything happens from there.

A short guided tour runs the first time, dimming the screen and pointing at each
part in turn. It is skippable, and **Show Onboarding** in the menu brings it back
whenever you want.

### 1. Add a project folder

Open the menu, then **Project Folders › Add Project Folder**, and pick the main
checkout of a git repository. Not a worktree of it, the checkout itself. Every
worktree of that repository then appears in the menu. The tour asks for this at
its second step, so following it along covers this.

You can add more than one project, and each keeps its own settings.

### 2. Decide what a click opens

**Settings › General › Apps** lists the editors, terminals and git clients it
found. Tick the ones you want offered, and set **Clicking a worktree opens** to
whichever should answer a plain click. Everything else stays one hold of ⌥ away.

If something you use is missing, **Add App** takes any app that can open a
folder.

### 3. Turn on Open at Login

**Open at Login** in the menu. A menu bar app you have to remember to start is
not much use.

### 4. Tell it where your worktrees live

**Settings › Project** holds the things that belong to a repository rather than
to your machine: which folder new worktrees are created in, and for Xcode
projects, what cloned simulators are named and whether deleting a worktree should
take its simulators and derived data with it.

Each project has its own, so a repository keeping worktrees in `.worktrees` and
another using something else can coexist.

### About permissions

Deleting a worktree offers to close windows still pointing at it. Xcode is asked
through its own scripting support; everything else goes through System Events,
which macOS gates behind Accessibility access. You will be asked the first time.
Declining costs only that one step, and nothing else in the app changes.

## Using it

- **Click** a worktree to open it in whichever app you chose.
- **Hold ⌥** on one for the full set of actions: every registered app, Finder,
  Copy Path, and Delete Worktree.
- **Manage Worktrees** shows every worktree of every project at once, with its
  branch, how far ahead or behind it is, its pull request, whether it is dirty,
  and the disk it holds. Several can be deleted together.
- **New Worktree** creates one for a new or existing branch, cloning the
  simulators it should get.
- **Storage** measures what Xcode is holding across derived data, simulators,
  device support and caches, and reclaims what nothing is using. Anything still
  backing a live worktree is marked in use so a bulk clean-up cannot take it.

Deleting a worktree removes the directory, and optionally its branch, its
simulators, and its derived data. The confirmation says exactly what is about to
go before anything happens.

## Updating

**Check for Updates** in the menu compares what you are running against the
latest release here, shows the notes, and installs it in place. The app quits,
swaps itself, and comes back on the new version. If the swap fails, the previous
copy is put straight back.

A background check runs at most once a day and reports only by relabelling that
menu entry to **Update to x.y.z**. Nothing is downloaded or replaced without
being asked for, and it can be turned off under **Settings › General › Updates**.

No account or token is involved at any point.
