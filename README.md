# Shard meta

Hosted data files read by [Shard Launcher](https://github.com/OhMarker/shard-launcher) at runtime.
The launcher fetches them from `raw.githubusercontent.com/OhMarker/meta/main/...`; a file that fails
validation is ignored and the launcher falls back to the copy it ships with. The full schema for every
file is in the launcher's `CONTRACT.md`.

| File | Purpose | How to update |
| --- | --- | --- |
| `shard-manifest.json` | Every published build of the Shard client jar. | Upload the jar to a [shard-client release](https://github.com/OhMarker/shard-client/releases), run `sha512sum` on it, add a build object and bump `latest`. |
| `bundled-mods.json` | The Shard Core mod set installed into every Shard instance. | Edit and bump `updatedAt`. Slugs are Modrinth project slugs. |
| `cosmetics.json` | The wardrobe catalogue. | Edit and bump `updatedAt`. `bundled://` textures ship inside the launcher; anything else must be an `https://` URL. |

Validate before committing:

```bash
node -e "for (const f of ['shard-manifest','bundled-mods','cosmetics']) JSON.parse(require('fs').readFileSync(f + '.json','utf8')); console.log('ok')"
```

Changes here take effect for every launcher the next time it starts or launches an instance. No
launcher release is needed.
