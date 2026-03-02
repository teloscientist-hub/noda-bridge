# noda-bridge

A static web mod for [NODA](https://noda.io/) — runs inside NODA's built-in Chromium browser and bridges your VR mind map with ClickUp.

## What it does

- **View & edit** NODA nodes and links in a dark-theme table UI
- **Live sync** from VR — node changes in the headset update the table in real time
- **ClickUp → NODA**: Pull your ClickUp workspace hierarchy (Spaces → Folders → Lists → Tasks) and push tasks as NODA nodes
- **NODA → ClickUp**: Push node title/description changes back to ClickUp tasks
- **Auto-sync** on a configurable interval (30s / 1min / 5min)

---

## Setup

### 1. Deploy to GitHub Pages

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Source: **Deploy from a branch**
4. Branch: `main`, Folder: `/ (root)`
5. Save — your page will be live at `https://<your-username>.github.io/noda-bridge/`

### 2. Enable NODA Web API

1. Put on your Meta Quest headset and open NODA
2. Go to **Settings → Console**
3. Enable **WebAPI**
4. Open the **Browser** from the NODA application menu
5. Navigate to your GitHub Pages URL

The page will connect automatically when opened inside NODA.

### 3. Connect to ClickUp

1. Get your ClickUp personal API token:
   - ClickUp → **Profile avatar → Apps → API token**
2. On the mod page, go to the **⚙ Settings** tab
3. Paste your token and click **Load Workspaces**
4. Select your **Workspace** and **Space**

> Your API token is stored in `localStorage` only — it is never sent to GitHub or any server other than ClickUp's API directly from your browser.

---

## Usage

| Tab | What you can do |
|-----|----------------|
| ⚙ Settings | Set ClickUp token, select Space, configure auto-sync |
| Nodes | Create, edit, delete NODA nodes; table updates live from VR |
| Links | Create, edit, delete links between nodes |
| ClickUp Sync | Fetch ClickUp hierarchy, push tasks to NODA, sync changes back |

### Sync workflow

1. Go to **ClickUp Sync** tab
2. Click **↓ Fetch from ClickUp** — loads all Folders/Lists/Tasks from your selected Space
3. Click **→ Push to NODA** — creates a node for each ClickUp task (skips tasks already in NODA)
4. Work in VR — add/move/edit nodes
5. Click **↑ Push changes to ClickUp** — updates ClickUp task names/descriptions from NODA nodes

---

## Phase 2: Custom Field Mappings

The current mapping (ClickUp Task → NODA Node) is a default scaffold:

| ClickUp field | NODA field | Current mapping |
|---------------|-----------|----------------|
| `task.name` | `title` | Direct copy |
| `task.description` | `notes` | Truncated to 300 chars + ClickUp ID tag |
| `task.status` | `color` | to do=gray, in progress=blue, done=green |
| `task.priority` | `shape` | urgent=Star, high=Diamond, normal=Ball, low=Box |
| `task.url` | `pageUrl` | Direct copy |

To apply your own mappings, edit the `clickupTaskToNodaNode()` and `nodaNodeToClickupTask()` functions in `index.html`.

---

## References

- [NODA Web API docs](https://noda.io/documentation/webapi.html)
- [NODA starter kit](https://github.com/beppert/Noda-Integration-API)
- [ClickUp API docs](https://clickup.com/api)
