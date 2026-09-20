# NEJE Software V3.6 — DK-8-KZ / DK-8-FKZ / NEJE-BL

An archive of **NEJE control software V3.6**, the last release before the V4
rewrite, for the discontinued NEJE DK-8-KZ and its siblings.

**NEJE no longer hosts V3.6, and it is still the latest fully compatible
software for these machines.**

NEJE does not distribute V3.6 any more. It is not on `neje.club`, not on
`neje.wiki`, and not on `wiki.nejetool.com`; those only go back as far as V4.0.
This repository is an unmodified personal copy, kept so that owners of these
machines have somewhere durable to get it.

If you came here searching for a **NEJE DK-8-KZ software download**, this is
**NEJE V3.6** — the version those machines were sold with.

## Why V3.6, and not something newer

V3.6 is the latest fully compatible software for this hardware and the one to
use — not a fallback, and not a historical curiosity. The "legacy" build NEJE
currently offers for these machines is severely cut down by comparison and
takes real effort to get talking to a DK-8-KZ at all. The current NEJE software
does not drive them at all. Nothing released after V3.6 is an upgrade for a
DK-8-KZ, DK-8-FKZ or NEJE-BL, which is why this archive deliberately points
nowhere else.

## What this is for

| Machine | Supported |
| --- | --- |
| NEJE DK-8-KZ (sold also as DK-8 PRO-5, JZ-5, JZ-6, DK-5 PRO-5) | yes |
| NEJE DK-8-FKZ | yes |
| NEJE-BL (NEJE's own documentation calls it DK-BL) | yes |

Windows only. The software is 32-bit and runs fine under emulation on Windows
on ARM, including in a VM on Apple Silicon.

## Contents

Everything below is exactly as it came from NEJE — nothing added, removed or
repacked.

| Path | Size | What it is |
| --- | --- | --- |
| `NEJE V3.6.exe` | 3.13 MiB | The application. PE32, .NET Framework 4.0, `ProductName` "NEJE LaserCarver", `FileVersion` 1.3.1.0, built 2017-10-15. Its welcome screen identifies itself as **NEJE V3.6**. It carries the per-firmware server files (V1.0, V2.0, V2.1, V3.0) and a copy of the driver internally. |
| `Driver.exe` | 238 KiB | WCH **CH341SER** USB-serial driver, a RAR self-extractor containing `SETUP.EXE`, `CH341SER.INF` (2014-08-08), `CH341SER.SYS` and `CH341S64.SYS` (2015-01-26), `CH341S98.SYS`, `CH341SER.VXD` and `CH341PT.DLL`. See the warning below before installing it. |
| `NEJE/V30.exe` | 350 KiB | The V3.0-firmware server file on its own, same 1.3.1.0 build as the copy inside the application. |
| `DK-8-KZ Manual.pdf` | 1.32 MiB | NEJE's 18-page user manual, dated 2017-09-19. Written a release earlier, so it names V3.5 as the support software. |
| `How to install the software in windows.docx` | 26 KiB | NEJE's own three-step install note. |
| `pic sample 490x490px/` | 2.0 MiB | 34 sample JPGs at the machine's native 490 × 490 px, plus `specification.txt`. |
| `SHA256SUMS.txt` | — | SHA-256 for all 40 files. Added by this archive; not part of the original bundle. |

No .NET Framework installer is included — NEJE's install note tells you to get
.NET 4.0 yourself, and on Windows 10 and 11 you already have it.

## Checking your download (optional)

You do not need this to use the software. It is here for one purpose: to let
you prove that the files you downloaded are byte-for-byte the files in this
repository, and not something altered on the way to you or re-uploaded
somewhere else. If you got them straight from this repository and that is good
enough for you, skip to [Installing](#installing).

To check, compare the SHA-256 of each file against the list below.

| File | SHA-256 |
| --- | --- |
| `NEJE V3.6.exe` | `8ea86420c5a1f65b4ef042b3fd1e95c4aab8adfce06470d0bc15092c595c2fda` |
| `Driver.exe` | `625841a5f3d2eceba4b0193124f31514ff706cd7b9919239b86161e6a298a945` |
| `NEJE/V30.exe` | `5ea6041d3037a49be9c464ffbfe8649fcb3e54e9d66dfa7508356f7176cc4841` |
| `DK-8-KZ Manual.pdf` | `49d8b54ae04efbc3caa29a910bcd5971c485e8cb3604ef1e1e251485f7f79f44` |
| `How to install the software in windows.docx` | `d54ed9d71662f9706807509907416b995e773817bdfa0d406c49db11f771f2c0` |

`SHA256SUMS.txt` covers all 40 files of the original bundle, sample images
included.

One file at a time:

```powershell
Get-FileHash -Algorithm SHA256 .\<file>
```

```sh
shasum -a 256 <file>
```

Or everything at once, from the root of a clone:

```sh
shasum -a 256 -c SHA256SUMS.txt
```

A hash that does not match means the file is not the one archived here — don't
run it. Separately, and expected: these are old unsigned binaries, so antivirus
heuristics may complain about them even when they are intact.

## Installing

1. **Install .NET Framework 4.0 first.** The application will not start
   without it. Windows 10 and 11 ship with a newer .NET Framework that
   satisfies this, so on those you can usually skip it.

2. **Do not install the bundled driver.** The archive includes `CH341SER`
   from 2014. It is unsigned, predates driver signature enforcement, and on
   Windows 10/11 it will either refuse to install or replace a working driver
   with a broken one. Modern Windows supplies the CH340 driver through Windows
   Update automatically, and macOS has included one since Big Sur.

3. **Confirm the laser enumerates, before you start the application.** Plug in
   the USB data cable and check Device Manager → Ports (COM & LPT). You want a
   `USB-SERIAL CH340 (COMx)` entry. If it is not there, fix that first — no
   version of the application can help you past a driver problem.

4. **Run the application.** There is no COM port to pick. It searches for the
   machine itself as it starts, shows "Auto Connecting…", and reports the
   result in its status pane. If it does not find the machine, the fault is
   the cable, the power or the driver — not the software.

## Notes

- The machine engraves from its own flash. The software uploads an image and
  settings, then the physical button on the unit starts the burn. You can
  unplug the computer once the upload finishes.
- Images go in at 490 × 490 px, which is the full 36.75 mm of the 38 × 38 mm
  work area at the machine's 0.075 mm step. The samples folder is already at
  that size.
- This is an open-beam diode laser — 405 nm on the DK-8-KZ. Eye protection
  rated for the module's wavelength, a nonflammable surface, ventilation, and
  don't leave it running unattended.

## Provenance

Downloaded in 2018 from NEJE's own download page, before the V4 rewrite
replaced it, and kept since. This is that download, unmodified: no file has
been altered, renamed, recompressed or removed, and nothing has been added
except this README and `SHA256SUMS.txt`.

The files carry their original timestamps of 2018-09-04, except `NEJE/V30.exe`,
which is stamped 2019-03-15.

## Legal

Not affiliated with, endorsed by, or connected to NEJE. The software is
NEJE's copyrighted work and is mirrored here unmodified, solely so that owners
of discontinued hardware can keep it working after the vendor withdrew the
download. No license is claimed or granted. If you hold the rights to this
software and would like it removed, open an issue or contact the repository
owner and it will be taken down.
