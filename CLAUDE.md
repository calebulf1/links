# links repo: Caleb's Amazon deep-link pages

## Story slots (most common request)
When Caleb sends an Amazon link and a slot number (e.g. "slot 2: https://a.co/d/xxxx", or just a link with no slot = slot 1):

1. Expand the link to the real product URL:
   `curl -Ls -o /dev/null -w '%{url_effective}' -A 'Mozilla/5.0 (iPhone; CPU iPhone OS 17_0 like Mac OS X) AppleWebKit/605.1.15 Mobile/15E148 Safari/604.1' '<link>'`
2. Build the deep link: keep only the amazon.com path (e.g. `https://www.amazon.com/dp/ASIN` or `/shop/calebulf/list/ID`), drop every tracking param, then append `?tag=calebulf-20`.
3. Write `story/<slot>/current.json` as exactly: `{"url":"<deep link>","set_at":<unix seconds now>}`
4. Commit and push to main. Reply with only the deep link and the slot page `https://calebulf1.github.io/links/story/<slot>/`. Nothing else.

Slots are 1-5. Slot pages add the Amazon app scheme and expire 24h after set_at. Never edit `story/<slot>/index.html` for a slot request.

## Everything else
- `go/index.html`: generic redirect, `?u=<url-encoded amazon url>`.
- Other folders: one-off deep-link pages per episode (template: copy any index.html, swap the list ID).
- Affiliate tag is always `calebulf-20`.
