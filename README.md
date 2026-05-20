# tkfdp.net

Landing page for the TKF-DP paper. Served via GitHub Pages from this repo
to the custom domain <https://tkfdp.net>.

## Contents

- `index.html` — the landing page
- `style.css` — site styling
- `supplement.pdf` — copy of the latest supplement PDF (built from
  [`evoldoers/tkfdp:math-paper/supplement.tex`](https://github.com/evoldoers/tkfdp/tree/main/math-paper))
- `supplement/` — browsable HTML rendering of the supplement, built
  with `make4ht`
- `CNAME` — GitHub Pages custom-domain marker

## Refreshing the supplement

The PDF and HTML are committed snapshots, not built on the GitHub
side. To refresh them after a supplement edit:

```bash
# 1. Build the PDF (in the tkfdp repo)
cd ~/tkf-dp/math-paper && bash build.sh --supp
cp supplement.pdf ~/path/to/tkfdp.net/

# 2. Build the HTML
mkdir -p /tmp/supp-html
rsync -a ~/tkf-dp/math-paper/ /tmp/supp-html/
cd /tmp/supp-html
rm -f main.aux  # disable \externaldocument to main (xr breaks tex4ht)
TEXINPUTS=".:./tkf-mixdom/tkf:" make4ht supplement.tex 'mathjax,2,sections+'
rsync -a --delete /tmp/supp-html/supplement*.html /tmp/supp-html/supplement*.css \
                  /tmp/supp-html/*.png /tmp/supp-html/*.svg \
                  ~/path/to/tkfdp.net/supplement/

# 3. Commit + push
cd ~/path/to/tkfdp.net && git add -A && git commit -m "Refresh supplement" && git push
```
