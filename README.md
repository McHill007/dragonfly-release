<div align="center">

<img src="docs/dragonfly-logo.svg" alt="DragonFly Logo" width="200" />

# DragonFly

**Lightweight project management for small teams.**\
Projects &middot; Todos &middot; Releases &middot; Notes &mdash; all in one native desktop app.

[![Latest Release](https://img.shields.io/github/v/release/McHill007/dragonfly-release?style=flat-square&color=00B4D8&labelColor=1a1a2e&label=latest)](https://github.com/McHill007/dragonfly-release/releases/latest)
[![Windows](https://img.shields.io/badge/platform-Windows-0078D6?style=flat-square&logo=windows11&logoColor=white&labelColor=1a1a2e)](https://github.com/McHill007/dragonfly-release/releases/latest)
[![Linux](https://img.shields.io/badge/platform-Linux-E95420?style=flat-square&logo=linux&logoColor=white&labelColor=1a1a2e)](https://github.com/McHill007/dragonfly-release/releases/latest)

---

### Download

> **[Latest Release](https://github.com/McHill007/dragonfly-release/releases/latest)**

| Installer | Description |
|-----------|-------------|
| `DragonFly.exe` | Portable Windows executable (no install needed) |
| `DragonFly_x.x.x_x64_en-US.msi` | Standard Windows Installer (MSI) |
| `DragonFly_x.x.x_x64-setup.exe` | NSIS Installer with **auto-update** support |
| `dragonfly_x.x.x_amd64.deb` | Debian / Ubuntu package |
| `dragonfly-x.x.x-1.x86_64.rpm` | Fedora / openSUSE package |
| `dragonfly_x.x.x_amd64.AppImage` | Portable Linux executable |

</div>

---

## Features

### Dashboard

Track your releases and features at a glance. See progress bars, task counts, and overall project health in one view.

<div align="center">
<img src="docs/dragonfly_screens/dashboard.gif" alt="Dashboard" width="800" />
</div>

<br/>

### Kanban Board

Drag & drop tasks across columns. Features group their child tasks together &mdash; moving a feature moves all its tasks along.

<div align="center">
<img src="docs/dragonfly_screens/board.gif" alt="Kanban Board" width="800" />
</div>

<br/>

### Tasks

Manage tasks and features with quick-add buttons, search, tags, and release assignment. Filter by release, feature, assignee, or tag.

<div align="center">
<img src="docs/dragonfly_screens/tasks.gif" alt="Tasks" width="800" />
</div>

<br/>

### Releases

Plan and organize your releases. Assign tasks, track progress, and generate CAB reports.

<div align="center">
<img src="docs/dragonfly_screens/release.gif" alt="Releases" width="800" />
</div>

<br/>

### Notes

Block-based rich text editor with hierarchical sub-notes, Table of Contents navigation, full-text search, tags, and file attachments.

<div align="center">
<img src="docs/dragonfly_screens/notes.gif" alt="Notes" width="800" />
</div>

<br/>

### Settings

Multi-language support (8 languages), customizable AI prompts, database backup, update check, user management, and optional sync configuration.

<div align="center">
<img src="docs/dragonfly_screens/settings.gif" alt="Settings" width="800" />
</div>

---

## Multi-Project Support

Create and manage multiple projects from a visual project selection screen. Each project has its own tasks, notes, releases, and sync configuration. Join shared projects from teammates via Sync URL + Space Key, or keep projects local-only.

---

## Your Server, Your Data

DragonFly works **fully offline** by default. All data stays on your machine.

For team sync, you self-host a [PocketBase](https://pocketbase.io) instance &mdash; your server, your rules. All synced data is **AES-GCM encrypted** with your space key before leaving the client. The server only stores opaque ciphertext.

### Quick Start

The `docker/` folder in this repository contains a ready-to-use `Dockerfile` and `docker-compose.yml`.

**1. Clone and start:**

```bash
git clone https://github.com/McHill007/dragonfly-release.git
cd dragonfly-release/docker
docker compose up -d --build
```

**2. Create a Superuser:**

```bash
docker exec dragonfly-pb /pb/pocketbase superuser create admin@example.com YOUR_PASSWORD
```

Or open the Admin UI at `http://localhost:8080/_/`.

**3. Connect DragonFly:**

In the app, go to **Settings > Sync** and enter:

| Field | Value |
|-------|-------|
| **Server URL** | `http://<your-server-ip>:8080` |
| **Admin Email** | The superuser email from step 2 |
| **Admin Password** | The superuser password from step 2 |
| **Space Key** | A shared passphrase (used for encryption + auth) |

Click **Setup Server** &mdash; DragonFly will automatically create all required collections and a sync user. After setup, click **Connect** to start syncing.

Teammates can **join** a synced project by entering the same Sync URL and Space Key in the Join Project dialog.

---

## Built with Modern Tools

| Layer | Technology |
|-------|------------|
| Runtime | [Tauri v2](https://v2.tauri.app) (Rust + WebView) |
| Frontend | React 18 + TypeScript + Vite |
| UI | Tailwind CSS v4 + shadcn/ui |
| Editor | BlockNote |
| State | Zustand |
| Sync | PocketBase (self-hosted) |

---

## Platform Notes

DragonFly is primarily developed and tested on **Windows**. Linux builds are provided as a convenience.

| Format | Tested on | Status |
|--------|-----------|--------|
| `.exe` / `.msi` | Windows 10/11 | Fully supported |
| `.deb` | Ubuntu 22.04+ | Works |
| `.rpm` | Fedora 36+ | Works |
| `.AppImage` | Ubuntu 22.04+ | Works |

> **Note:** RHEL-based distributions (Oracle Linux, CentOS, Rocky Linux) may lack the required `libwebkit2gtk-4.1` library. Use the AppImage on those systems or try Fedora instead.

If you run into problems on your Linux distribution, please [open an issue](https://github.com/McHill007/dragonfly-release/issues).

---

## Changelog

### v0.1.5

**Features**
- Multi-project support with visual project selection screen (create, edit, delete, switch)
- Join shared projects from teammates via Sync URL + Space Key
- Table of Contents panel for Notes (click headings to navigate)
- Collapsible tag section in Notes with inline tag editing
- Customizable AI prompts for notes, tasks, and CAB reports in Settings
- Leave project option for synced projects (removes local copy, keeps remote)
- Per-project sync credentials (each project can use a different server)

**Improvements**
- Attachments cleaned up when deleting a project
- Sync credentials cleared on project leave/delete to prevent ghost reconnects
- Project metadata (name, description, color) syncs to remote

**Bugfixes**
- Fixed tombstone reconnect loop that repeatedly tried to sync deleted projects
- Fixed project leave functionality not properly disconnecting sync

---

### v0.1.4

**Features**
- Collapsible sidebar (240px / 56px) with icon tooltips and smooth transition
- Collapsible Kanban columns with rotated text strip and drag-drop support
- Default collapsed columns configurable in Settings (persisted to database)
- Horizontal scroll on the board with min-width per column
- Settings reorganized into 5-tab system (General, Users, Data, Sync, About)
- License and third-party license info in About tab

**Improvements**
- Compact TaskCard design: smaller tags, release as text, avatar next to title
- Standardized font sizes across Dashboard, Tasks, and Releases pages
- Responsive toolbars with horizontal scroll and smaller controls
- Board usable at smaller window sizes (min-width reduced to 800px)

---

### v0.1.3

**Features**
- Update check in Settings (checks GitHub releases for new versions)
- Quick-add buttons on release headers and feature rows in Tasks view
- Search field to filter tasks by title
- CAB report generation for releases

**Improvements**
- TaskModal accepts initial release/feature values for pre-filled creation
- Linux CI builds fixed (icons included in repo)

---

### v0.1.1

**Features**
- Database backup (ZIP with DB + attachments) in Settings
- Recycle bin for tasks and notes with restore/permanent delete
- Delete confirmation dialogs for tasks, notes and releases
- Deleting a feature asks whether to also delete child tasks
- Tasks grouped under their feature in the board
- Dragging a feature moves all child tasks along
- Show/hide done toggle on the board
- Feature modal shows list of child tasks
- Dashboard with release and feature progress overview
- CSV export for tasks
- 6 new languages: Polish, French, Spanish, Italian, Romanian, Hindi
- Linux builds (DEB, RPM, AppImage)
- Portable Windows EXE in releases

**Improvements**
- Releases sorted descending in filter dropdowns
- Features sorted alphabetically in filter dropdown

**Bugfixes**
- Fixed build error caused by unsupported Array method

---

### v0.1.0

**Features**
- PocketBase sync with end-to-end encryption
- Passphrase protection with auto-lock
- Hierarchical notes with sub-notes
- AI text improvement (OpenAI integration)
- File attachments for tasks and notes
- Kanban board with drag-and-drop
- Features and tasks (two-level hierarchy)
- Release management with task assignment
- User management with color avatars
- Tags for tasks
- Automated build and release via GitHub Actions
