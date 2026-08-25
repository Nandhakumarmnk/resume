# Nandhakumar M — Résumé

Source and build for the résumé of **Nandhakumar M**, Senior .NET Full-Stack Developer —
React.js, ASP.NET Core, C#.

**Portfolio:** <https://nandhakumarmnk.github.io/>
**LinkedIn:** <https://linkedin.com/in/nandhakumar-m-dotnet>

## Files

| File | Purpose |
|---|---|
| `Nandhakumar_M_Senior_DotNet_FullStack_Resume_v4.html` | The source. Single self-contained file — HTML plus an inline print stylesheet, no dependencies. |
| `Nandhakumar_M_Senior_DotNet_FullStack_Resume_v4.pdf` | The built PDF. This is the file to attach to applications. |

The same PDF is served from the portfolio's "Download Résumé" buttons as
`Nandhakumar_M_Resume.pdf` — update it there whenever this one changes.

## Building the PDF

The HTML is laid out for A4 with `@page { size: A4; margin: 9mm 11mm; }`. Any Chromium
browser in headless mode produces the PDF:

```bash
# Windows / Edge
"C:/Program Files (x86)/Microsoft/Edge/Application/msedge.exe" \
  --headless=new --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="Nandhakumar_M_Senior_DotNet_FullStack_Resume_v4.pdf" \
  "file:///D:/Resume/Nandhakumar_M_Senior_DotNet_FullStack_Resume_v4.html"
```

`--no-pdf-header-footer` matters — without it Chromium stamps a URL and date onto every page.

Or just open the HTML and `Ctrl+P` → Save as PDF, margins **None**, background graphics **on**.

## Editing

Everything is plain HTML in one file. The structure is:

- `<header>` — name, headline, contact line. The contact line is deliberately label-free
  (`linkedin.com/... | github.com/... | nandhakumarmnk.github.io`) so all three fit on one
  line; adding `LinkedIn:` / `GitHub:` / `Portfolio:` prefixes pushes it to three.
- `.skill` — one row per skill category. Order is intentional:
  **Frontend (Modern) → Frontend (Server-Side) → Backend → Database → Cloud/DevOps →
  Security/Integration → Practices/AI**. React and TypeScript lead; jQuery, Razor, and
  DevExtreme sit in the server-side row so the profile does not read as legacy MVC.
- `.role` + `.org` + `<ul>` — one block per job.
- `.proj-block` — one block per project. Vendor Portal is first because it carries the
  React evidence.

## Keep it to two pages

The layout is tuned to fill exactly two A4 pages. After editing, rebuild and check:

```bash
pdftotext -layout Nandhakumar_M_Senior_DotNet_FullStack_Resume_v4.pdf - | tr -cd '\f' | wc -c
# prints 1 → 2 pages
```

If it spills to three, trim bullets rather than shrinking `body { font-size }` below 9pt.

## Claims to keep defensible

Some wording is deliberate and should not drift back:

- **"500+ security issues/findings"** — not "vulnerabilities", which implies formal
  verification that has not happened.
- **"meeting agreed SLA commitments"** — not "no SLA breaches", which is an absolute
  claim that cannot be objectively proven in an interview.
- **Zero-downtime deployment** always appears with its mechanism — scheduled off-peak
  windows, pre-tested rollback scripts, post-deployment validation. The claim is only
  credible when the how is stated.
- **React and TypeScript** appear only on the Vendor Portal. The Enterprise Supply Chain
  project stays JavaScript/jQuery because that is what it actually used.
