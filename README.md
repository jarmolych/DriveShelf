# DiskShelf

Track your drives, plan your bays and RAID pools, from a pile of disks to a rack of servers.

DiskShelf is a single-file web app. Open `index.html` in any modern browser: nothing to install, no build step, no server, no account.

## Who it's for

On first launch DiskShelf asks what you're planning and sets itself up to match:

- **Just my drives**: a drive inventory with RAID pool planning, no servers or bays. Good for a drawer of disks, a desktop, or deciding what to buy.
- **One or more servers**: add servers from templates (generic 4 to 24-bay, Dell PowerEdge T320 and R720xd, HPE MicroServer, Synology DS920+ and DS1821+, Supermicro SC846, NetApp DS4246), or pick **Custom** and enter any bay count from 1 to 96.
- **Show me an example**: sample data with two servers and 14 drives to look around.

Nothing is locked in. Add or remove servers any time, or reopen the setup from **Settings → Data → Change setup**. Your drives, pools and notes are kept.

## Features

- **Drive inventory**: track drives by ID, size, type (HDD/SSD), make, form factor and last 4 of the serial. Rows, compact, tile and by-vdev views, filters, search, bulk add and bulk edit.
- **Servers and bays**: up to 24 servers with 1 to 96 bays each, drawn as chassis with drive sleds. Rename, resize, reorder or remove servers; click, shift-click and drag sleds to place, swap and eject drives, including between servers.
- **Vdevs and pools**: ZFS stripes, mirrors and RAIDZ1/2/3, or classic RAID 0/1/5/6/10. Usable space, redundancy, wasted space and failure tolerance update live, with warnings for risky layouts, mixed drive sizes, mixed HDD/SSD, and pools split across servers.
- **Datasets and space**: per-pool usage ring, dataset breakdown, encryption flags and diagrams of how data and parity stripe across drives.
- **Bay combos**: pool layouts generated from your own inventory and sized to fit your bays. Each pool is kept in one server, and drives noted as dead, failing or locked are left out.
- **Saved layouts and notes**: snapshot different plans and switch between them; attach notes to drives, vdevs and pools.
- **Customizable UI**: drag-and-drop section grid, saved views, 40+ themes, density and scale settings.
- **Undo** for every change that moves or removes data.

## Saving

Changes save automatically to your browser's local storage. Use **Save file** to export everything (drives, servers, pools, notes, saved layouts and settings) as a `.json` file, and **Load file** to restore it on any device.

Files from the earlier single-server T320 Pool Planner and the multi-server RAID Planner load too.

## How it works

Everything lives in `index.html`: plain HTML, CSS and JavaScript with no dependencies.

Bays across all servers are stored as one flat array, and each server owns a contiguous slice of it. Drive placement, selection, drag-and-drop and undo work the same within a server and across servers, and a drives-only inventory is simply the case of zero servers. Setup choices only change data (which servers exist, which sections are visible), so there's a single code path for every kind of user.
