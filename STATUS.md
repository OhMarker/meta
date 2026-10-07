# Status (handoff for a new session)

Last updated 2026-10-07.

- Prepared locally by Claude; NOT on GitHub yet. Claude's sandbox is not allowed to create public
  repositories, so the owner runs the publish step below. The launcher reads these files from
  `https://raw.githubusercontent.com/OhMarker/meta/main/<file>` (see CONTRACT.md in shard-launcher).
- `shard-manifest.json` lists client 0.2.0 for Minecraft 1.21.11 with the sha512 of
  `../shard-client/build/libs/shard-0.2.0.jar`. Its `url` points at the shard-client v0.2.0
  release asset, which must be created first (see ../shard-client/STATUS.md). 0.1.0 was never
  published, so it is not listed.
- `bundled-mods.json` and `cosmetics.json` are exact copies of the launcher's shipped files
  (`src/main/mods/bundled-mods.json`, `resources/cosmetics/cosmetics.json`).

## Publish (owner runs once, from this folder, after the shard-client release exists)

```bash
gh repo create OhMarker/meta --public --source=. --remote=origin --push --description "Hosted data files for Shard Launcher: client manifest, bundled mod set, cosmetics"
```

Then confirm the launcher sees it: `curl -s https://raw.githubusercontent.com/OhMarker/meta/main/shard-manifest.json`
should print the manifest, and a Shard 1.21.11 instance in the launcher should switch from
"Client pending" to installing `shard-0.2.0.jar` on the next launch.
