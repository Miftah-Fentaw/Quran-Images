# Contributing to Quran Images

Thank you for taking the time to improve this archive. Quran Images is a shared set of mushaf page files, and careful contributions keep it useful for people building readers.

Questions, corrections, and pull requests are welcome. Please be kind, assume good faith, and keep the discussion on the files and the docs.

## How to propose a change

1. Look through the [open issues](https://github.com/Miftah-Fentaw/Quran-Images/issues) so the same idea is not already being discussed.
2. For anything that would touch the page images, open an issue first and wait for a response.
3. Fork the repository and create a branch from `main`.
4. Make the change. Docs, the banner, and small pieces of tooling can be opened directly as a pull request.
5. Open the pull request against `main` and describe what changed and why.

There is no build step. The repository is the images plus these documents.

## Pull requests

A good pull request is easy to review:

- Keep it focused. A docs fix and a new script can be separate requests when they are unrelated.
- Say which files you changed, and which page numbers you checked if you mention the mushaf.
- Leave `png/` and `webp/` byte-for-byte alone unless an issue has already agreed that one named file is missing or damaged.
- Match the tone of the README: clear, accurate, and respectful.
- If you change `assets/banner.png`, keep it geometric. No pictures of people or prophets.

The maintainer may ask for a smaller diff or a clearer explanation before merging.

## What belongs here

- Corrections to the README, this guide, or the issue template, when they match the files that are actually in the repo.
- Notes and small tools that help an app load the existing pages, without rewriting those pages.
- A report of a missing, truncated, or unreadable page, with the folder and the page number.
- Fixes to the banner or other non-page assets.

## What to leave unchanged

Please do not recompress, resize, re-encode, or replace the page corpus as a cleanup. The `png/` and `webp/` folders are the archive. A well-meant re-export changes every file, makes review impossible, and can harm the text.

Also out of scope for this repository:

- Translations, tafsir, audio, or recitation.
- Religious debate. This archive distributes page images; it is not a place to argue belief.
- A second copy of the pages under a new folder name, unless an issue has agreed the layout should change.

If a single page is truly damaged, open an issue, name the file (`png/120.png`, `webp/120.webp`, and so on), and describe what is wrong. Wait for a decision before replacing it.

## Reporting an issue

Open an issue and include:

- What you expected, and what you found.
- The folder and page number, when the report is about an image.
- Your app or viewer, if a file opens in one place and fails in another.
- A screenshot when the problem is visual.

Pages are numbered as mushaf pages. `png/1.png` and `webp/001.webp` are the same page. `webp/000.webp` is the extra Bismillah plate and has no PNG twin.

## Tone

Speak to other people the way you would want a guest treated in a place where the Quran is being shared. Disagree about a file or a sentence, not about the person. No harassment, and no sneering at anyone's school, language, or level of knowledge.

If a conversation stops being about the project, step away and let a maintainer close it.
