# My Mathematics Bookshelf

A static bookshelf site for GitHub Pages: no build step, no server. Open `index.html` and it reads the catalog in `books.json`.

## Adding a book

Add an entry to `books.json`:

```json
{
  "title": "Topology",
  "subtitle": "Second Edition",
  "author": "James Munkres",
  "year": 2000,
  "topics": ["Topology"],
  "pages": 537,
  "note": "Optional one-line description shown in list view.",
  "file": "books/munkres-topology.pdf"
}
```

Only `title` and **one source** are required. The source can be one of:

| Field   | Example                                          | Where the PDF lives                                                      |
|---------|--------------------------------------------------|---------------------------------------------------------------------------|
| `file`  | `"books/x.pdf"`                                  | In this repo                                                             |
| `url`   | `"https://github.com/<you>/bookpdfs/releases/download/v1/x.pdf"` | Any direct PDF link: a GitHub Release, R2, Internet Archive and so on |
| `drive` | `"1AbCdEfGhIjK…"`                                | Google Drive, with sharing set to "Anyone with the link"                 |

A PDF uploaded to `books/` without a `books.json` entry still appears on the site, under an "Uncatalogued" topic and titled from its filename.

Cover icons depend on the first topic: Analysis ∫, Geometry ∇, Proofs ∎, Olympiad ∑, Problem Solving ?, Algebra ≅, Number Theory ℤ, Combinatorics !, Topology ∮, Probability ℙ, Linear Algebra λ. You can override them per book with `"glyph"` and `"color"`.

---

## Free storage when the repo fills up

**How much room is left:** GitHub suggests keeping a repo under 1 GB and blocks any single file over 100 MB. A GitHub Pages site can be at most 1 GB. Today the PDFs use about 30 MB, which leaves room for roughly 30 more books of this size. Deleted files stay in the git history, so deleting a PDF does not free space in the repo.

### Option 1: GitHub Releases (recommended, nothing new to sign up for)
- Free, with no total storage limit and no bandwidth cap. Each file can be up to 2 GB.
- The files don't count toward the repo size or the 1 GB Pages limit.
- Downside: GitHub serves these files as downloads, so they can't open in the built-in reader. **Read** opens them in a new tab, and the browser downloads them first.

How to use it:
1. On GitHub, go to **Releases → Draft a new release**. Create a tag such as `books-v1` and drag in the PDFs. You can add more files to the same release later.
2. Right-click a file and copy its link. It looks like `https://github.com/madhupbhardwaj/bookpdfs/releases/download/books-v1/x.pdf`.
3. Put that link in `books.json` as `"url"`.

### Option 2: Google Drive (best for reading on a phone)
- 15 GB free, shared with Gmail and Photos.
- Opens inside the site's reader on every device, including phones, using Drive's own viewer.
- Steps: upload the PDF, then **Share → Anyone with the link**. Copy the ID from the link (`drive.google.com/file/d/<ID>/view`) and set `"drive": "<ID>"`.

### Option 3: Cloudflare R2 (most "proper", if you need lots of space)
- 10 GB free each month, with no download (egress) fees. Files are served as real PDFs, so they open in the browser.
- Needs a Cloudflare account with a payment method on file. Below 10 GB you aren't charged.
- Create a bucket, turn on its public `r2.dev` URL, upload the files and use `"url"`.

### Also possible
- **Backblaze B2**: 10 GB free. It works like R2.
- **Internet Archive (archive.org)**: free and unlimited, but everything is public and it removes copyrighted books. Use it only for public-domain titles such as Hardy.
- **Avoid Git LFS**: GitHub Pages doesn't serve LFS files, and the free quota is small.

> Note: this repo and site are public. Hardy's *Course of Pure Mathematics* is in the public domain, but most of the other books are still under copyright. If you want to keep those private, Google Drive with restricted sharing or a private R2 bucket is safer than a public repo.
