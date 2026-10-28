![Quran Images banner: an emerald header with gold geometric rosettes and the words القرآن الكريم](assets/banner.png)

# Quran Images

[![MIT License](https://img.shields.io/badge/license-MIT-0E3F32?style=flat-square)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/Miftah-Fentaw/Quran_webp?style=flat-square&color=0E3F32&label=stars)](https://github.com/Miftah-Fentaw/Quran_webp/stargazers)
[![Last commit](https://img.shields.io/github/last-commit/Miftah-Fentaw/Quran_webp?style=flat-square&color=0E3F32)](https://github.com/Miftah-Fentaw/Quran_webp/commits/main)

Quran Images is an open-source set of **Quran page images** for the full mushaf. It holds all **604 pages**, as compact PNG files and as higher-resolution WebP files, so a mobile app, a desktop app, or a page viewer can ship a readable mushaf **offline**.

Each page is one file. A reader loads the page on screen, keeps a neighbor ready, and leaves the rest on disk. The project is released under the [MIT License](LICENSE).

## Contents

- [Quick start](#quick-start)
- [What this is](#what-this-is)
- [Why these pages exist](#why-these-pages-exist)
- [Features](#features)
- [Repository layout](#repository-layout)
- [Using the images](#using-the-images)
- [Attribution](#attribution)
- [License](#license)
- [Contributing](#contributing)

## Quick start

```bash
git clone https://github.com/Miftah-Fentaw/Quran_webp.git
```

| You want | Open |
| --- | --- |
| First mushaf page (Al-Fatiha), compact | `png/1.png` |
| Same page, transparent WebP | `webp/001.webp` |
| Opening of Al-Baqarah | `png/2.png` or `webp/002.webp` |
| Final page (Al-Ikhlas, Al-Falaq, An-Nas) | `png/604.png` or `webp/604.webp` |
| Bismillah plate (WebP only) | `webp/000.webp` |

Put a WebP page on a light background. The ink is dark and the rest of the file is transparent.

## What this is

This repository publishes the standard 604-page mushaf as ordinary images. The archive is the page files themselves: two renditions, grouped by format, with any chapter map left to the app.

- `png/` is the small set. About **32 MB** for every page, suitable for a tight app bundle.
- `webp/` is a fixed **1080×1440** transparent set. About **180 MB**, suited to a layout that paints its own page color.

`png/1.png` is the illuminated opening page (Al-Fatiha). `png/2.png` opens Al-Baqarah. `png/604.png` closes with Al-Ikhlas, Al-Falaq, and An-Nas. The WebP file with the same page number shows that same page as dark ink on transparency. `webp/000.webp` is an extra front image, a large calligraphic Bismillah (`بسم الله الرحمن الرحيم`), and it has no file in `png/`.

## Why these pages exist

A mushaf viewer needs a page it can address by number, store on the device, and decode one at a time.

- **Size.** The PNG set averages about 54 KB a page (about 44–84 KB). The whole mushaf is small enough to bundle or to download once.
- **A stable canvas.** Every WebP file is 1080×1440, with an alpha channel, so the app chooses the paper color.
- **Readability.** These are full mushaf pages, with the familiar page breaks, not a reflowed extract.
- **Offline reading.** After the chosen folder is on disk, turning the page does not need a network.
- **A simple contract.** Page 1 is page 1 in both folders. An integrator does not have to parse a manifest.

## Features

- All 604 mushaf pages, with no missing numbers in either folder
- Compact indexed-color PNG pages for download size and memory
- Higher-resolution transparent WebP pages at one pixel size
- One file per page, so a viewer can load, cache, and release pages on its own
- An additional WebP Bismillah plate at `webp/000.webp`
- [MIT License](LICENSE), with attribution of the high-resolution source

## Repository layout

```text
.
├── LICENSE
├── README.md
├── CONTRIBUTING.md
├── assets/
│   └── banner.png          # header used at the top of this README
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── issue.md
├── png/                    # 604 files: 1.png … 604.png
└── webp/                   # 605 files: 000.webp … 604.webp
```

Files are grouped by format only. A chapter is not a directory.

### `png/`

| | |
| --- | --- |
| Files | `1.png` through `604.png` (604 files, none missing) |
| Names | Page number with no zero-padding: `1.png`, `10.png`, `604.png` |
| Appearance | Opaque illuminated mushaf pages, with ornamental borders and a paper ground |
| Color | Indexed-color PNG (8-bit palette) |
| On disk | About 32 MB total. About 44–84 KB per page, average about 54 KB |
| Pixel size | Pages 1 and 2 are 442×645. Pages 3–604 vary from 482–497 px wide and 790–814 px tall |

Do not assume one pixel size for every PNG page. Read the file's own dimensions.

### `webp/`

| | |
| --- | --- |
| Files | `000.webp` through `604.webp` (605 files, none missing) |
| Names | Three digits: `001.webp`, `010.webp`, `604.webp` |
| Pixel size | Every file is 1080×1440 |
| Appearance | Dark ink on a transparent background (WebP with an alpha channel) |
| On disk | About 180 MB total. About 57–360 KB per page, average about 305 KB |

`webp/000.webp` is the Bismillah plate, not a 605th mushaf page. Pages **1 through 604** share one numbering across the two folders. `png/1.png` and `webp/001.webp` are Al-Fatiha, `png/2.png` and `webp/002.webp` open Al-Baqarah, and `png/604.png` and `webp/604.webp` are the final page.

A black backdrop hides this ink. Composite the WebP onto white, cream, or the app's page color.

## Using the images

Load one page at a time. Decoding all 604 images at startup spends memory the reader will not use.

For day-to-day development, raw files are served from this repository:

```text
https://raw.githubusercontent.com/Miftah-Fentaw/Quran_webp/main/png/1.png
https://raw.githubusercontent.com/Miftah-Fentaw/Quran_webp/main/webp/001.webp
```

Ship a copy inside the app, or mirror the folder you chose, for a production reader. Offline use should not depend on GitHub staying reachable.

### Load a page

```text
png/{page}.png          page is 1..604, no padding
webp/{page:03d}.webp    page is 0..604, three digits
```

```javascript
function pngPath(page) {
  if (page < 1 || page > 604) {
    throw new RangeError("PNG pages run from 1 to 604");
  }
  return `png/${page}.png`;
}

function webpPath(page) {
  if (page < 0 || page > 604) {
    throw new RangeError("WebP files run from 000 to 604");
  }
  return `webp/${String(page).padStart(3, "0")}.webp`;
}
```

```dart
String pngPath(int page) => 'png/$page.png'; // 1..604

String webpPath(int page) =>
    'webp/${page.toString().padLeft(3, '0')}.webp'; // 0..604
```

### Load a chapter

Surahs are not stored as their own images. A chapter is a run of mushaf pages, and more than one surah can share a page. The map from surah to page is not in this repository. Keep that small index in the app, point it at a page number, and load the file with the helpers above.

A practical sequence:

1. Store the first mushaf page of each surah in the app.
2. When the reader opens a surah, resolve it to that page.
3. Load the image, and prefetch the next page.
4. Drop pages that have moved well off screen.

The landmarks checked in this archive: page 1 is Al-Fatiha, page 2 begins Al-Baqarah, and page 604 contains Al-Ikhlas, Al-Falaq, and An-Nas. A surah that begins in the middle of a page still uses that whole page image.

### Caching and offline reading

- Cache by the full relative path. `png/2.png` and `webp/002.webp` are different pictures of one page, so they need different cache entries.
- Keep the open page decoded, plus one or two neighbors. That is enough for a smooth turn.
- For an offline app, copy the chosen folder into the bundle, or download it once and keep it in local storage. Later reads stay on disk.
- Prefetch the next page when the reader settles, not all remaining pages.

### Which folder to ship

| Need | Use |
| --- | --- |
| Smallest download and a finished, illuminated page | `png/` (about 32 MB) |
| One canvas size, and a background the app controls | `webp/` (about 180 MB) |
| A decorative opening plate | `webp/000.webp` only |

PNG dimensions change slightly from page to page. WebP dimensions do not. Pick one folder per viewer rather than mixing them on the same spread, or the page frame will jump.

## Attribution

The original high-resolution pages come from **[Quran-PNG](https://github.com/GovarJabbar/Quran-PNG)** by [GovarJabbar](https://github.com/GovarJabbar).

That repository describes its files as full-quality PNG pages generated by [quran.com-images](https://github.com/quran/quran.com-images). This repository publishes a compact PNG rendition and a transparent WebP rendition, arranged in `png/` and `webp/`.

## License

This project is [MIT](LICENSE) licensed.

Copyright (c) 2026 [Miftah Fentaw](https://github.com/Miftah-Fentaw) (`@Miftah-Fentaw`).

You may use, copy, modify, and ship this repository under those terms. Keep the copyright notice and the license text with any substantial copy. The terms are the standard MIT License reproduced in [LICENSE](LICENSE).

[Quran-PNG](https://github.com/GovarJabbar/Quran-PNG) does not include a license file. The MIT terms here apply to this repository as published by Miftah Fentaw. Please leave the attribution above intact when you redistribute the pages.

## Contributing

Corrections, clearer docs, and small tools are welcome. Please do not recompress or replace the page images as a casual cleanup. The guide for issues and pull requests is [CONTRIBUTING.md](CONTRIBUTING.md).

All praise is due to Allah, who sent down the Quran and preserved it. May these pages be of use to anyone building a sincere reader.
