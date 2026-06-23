# tkfdp.net

Landing page for the TKF-DP paper. Served via GitHub Pages from this repo
to the custom domain <https://tkfdp.net>.

## Contents

- `index.html` — the landing page
- `style.css` — site styling
- `supplement.pdf` — copy of the latest supplement PDF (built from
  [`evoldoers/tkfdp:math-paper/supplement.tex`](https://github.com/evoldoers/tkfdp/tree/main/math-paper))
- `CNAME` — GitHub Pages custom-domain marker

> **Note:** the browsable LaTeX→HTML rendering of the supplement (the old
> `supplement/` directory, built with `make4ht`) has been **removed** — the
> conversion was broken and unreadable. The supplement is offered as PDF only.

## Refreshing the supplement

`supplement.pdf` is a committed snapshot, not built on the GitHub side.
To refresh it after a supplement edit:

```bash
# Build the PDF in the dev tree
cd ~/tkf-dp/math-paper && bash build.sh --supp
cp supplement.pdf ~/path/to/tkfdp.net/

# Commit + push
cd ~/path/to/tkfdp.net && git add -A && git commit -m "Refresh supplement" && git push
```
