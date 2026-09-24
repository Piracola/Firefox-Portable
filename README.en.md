<div align="center">

# Firefox Portable

Ready-to-run Firefox Windows x64 portable build. Data stays in the folder; nothing is written to the registry.

[![Release][badge-release]][link-release]
[![Downloads][badge-downloads]][link-release]
[![Build][badge-build]][link-actions]
[![License][badge-license]][link-license]

**[⬇ Download latest][link-release]** · **[📖 User guide][link-usage]**

[简体中文](README.md) | **English**

</div>

> Build system: [Gecko-Portable](https://github.com/Piracola/Gecko-Portable) — this repository is only one of its build configs.

## Navigation

- [Latest release](https://github.com/Piracola/Firefox-Portable/releases/latest): grab `Firefox_<version>.7z`
- [User guide](./docs/usage.md): layout, config, verification
- [Development](./docs/development.md): CI and local builds
- [Gecko-Portable](https://github.com/Piracola/Gecko-Portable): shared builder
- [Floorp_portable](https://github.com/Piracola/Floorp_portable) · [Zen-Portable](https://github.com/Piracola/Zen-Portable)

## About

The browser comes straight from Mozilla's official installer and is made portable with [libportable](https://github.com/adonais/libportable): all data stays inside the extracted folder, nothing is written to the registry, and you can carry it on a USB stick. GitHub Actions rebuilds daily to track official releases.

## Features

- Profile data in `Profiles/`, cache in `Cache/` next to the browser
- No registry writes — delete the folder to uninstall
- Runs from removable media
- Every release ships a `.sha256` checksum
- Injection check + real portability smoke test before publish

## Quick start

**Install**

1. Open the [latest release](https://github.com/Piracola/Firefox-Portable/releases/latest)
2. Download `Firefox_<version>.7z` (**not** `Source code`)
3. Extract anywhere, e.g. `D:\Browser\Firefox`
4. Double-click `开始.bat` to create a shortcut, then launch via that shortcut

**Update**

1. Close Firefox completely
2. Rename the old `Firefox` folder to `Firefox_old`
3. Extract the new `Firefox` folder in place (**keep `Profiles/`**)
4. Confirm data is intact, then delete `Firefox_old`

**Uninstall**

Delete the whole extracted folder after backing up `Profiles/` if needed.

## FAQ

**Which file do I download?**  
`Firefox_<version>.7z`. `Source code` is not a browser.

**Where is my data?**  
`Profiles/` next to the browser folder.

**Can I run it from a USB drive?**  
Yes. Prefer a short path such as `U:\Firefox`.

**Antivirus alert?**  
Portable patching rewrites module imports and is often a false positive. Download only from this repo's Releases and verify the `.sha256` hash.

**English UI?**  
Add a language pack in `Settings → General → Language`, or build with `--lang zh-CN`.

More in the [user guide](./docs/usage.md).

## Related projects

| Project | Notes |
| --- | --- |
| [Gecko-Portable](https://github.com/Piracola/Gecko-Portable) | Shared builder |
| [Floorp_portable](https://github.com/Piracola/Floorp_portable) | Portable Floorp |
| [Zen-Portable](https://github.com/Piracola/Zen-Portable) | Portable Zen |
| [libportable](https://github.com/adonais/libportable) | Upstream portable runtime |

## License

MIT — see [LICENSE](LICENSE).

Firefox is a trademark of the Mozilla Foundation; the browser itself remains copyright Mozilla. The libportable component is covered by its own license and ships with the package.

---

<div align="center">

<sub>Built and maintained by</sub>

**Piracola**

</div>

[badge-release]: https://img.shields.io/github/v/release/Piracola/Firefox-Portable?display_name=tag&style=flat-square&color=d8653f&label=Release
[badge-downloads]: https://img.shields.io/github/downloads/Piracola/Firefox-Portable/total?style=flat-square&color=2ea043&label=Downloads
[badge-build]: https://img.shields.io/github/actions/workflow/status/Piracola/Firefox-Portable/Firefox-Portable-Package.yml?branch=main&style=flat-square&label=Build
[badge-license]: https://img.shields.io/github/license/Piracola/Firefox-Portable?style=flat-square&color=6e7681&label=License

[link-release]: https://github.com/Piracola/Firefox-Portable/releases/latest
[link-usage]: ./docs/usage.md
[link-actions]: https://github.com/Piracola/Firefox-Portable/actions/workflows/Firefox-Portable-Package.yml
[link-license]: https://github.com/Piracola/Firefox-Portable/blob/main/LICENSE
