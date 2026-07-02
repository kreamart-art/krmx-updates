# krmx-updates

Statische update- en downloadsite voor de KRMX Audio plugins, live op
https://krmx.artnomad.nl (nginx op Coolify/Hetzner).

## Structuur

- `site/smplr/version.json` — gepolld door de UPDATE knop in SMPLR
- `site/smplr/SMPLR-x.y.z-mac.{pkg,dmg,sha256}` — de installers zelf
- `site/smplr/index.html` — downloadpagina met Gatekeeper-uitleg

## Nieuwe release publiceren

1. In de KRMX repo: bump `project(KRMX VERSION x.y.z)` in de root CMakeLists,
   bouw, en run `./installer/macos/build-installer-adhoc.sh`. Dat levert in
   `dist/`: pkg, dmg, sha256 en een kant-en-klare `version.json`.
2. Kopieer die vier bestanden naar `site/smplr/` hier (oude installers mogen
   weg; version.json overschrijven).
3. Werk de versienummers in `site/smplr/index.html` bij.
4. Commit, push, en trigger de Coolify deploy (zelfde token-dance als de
   andere apps, app: krmx-updates).

De plugin vergelijkt `version.json.version` met zijn eigen ingebouwde versie
en biedt `version.json.pkg` als download aan.
