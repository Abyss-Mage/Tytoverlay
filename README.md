# TYTGEAR Overlay Studio

An animated creator name tag and TYTGEAR product drops for OBS, with a web editor. Everything is in one file, `index.html`.

## For creators

1. Open the editor (`index.html`, or the GitHub Pages URL once Pages is enabled).
2. Fill in your name and TYTGEAR creator code, then pick a finish, typeface and animations.
3. Press **Copy OBS link**. In OBS add **Sources → + → Browser**, paste the link and use the size the editor shows.
4. Optional: under **Product drops**, choose **Separate link** to get a second link that shows only product drops, so you can place them anywhere on screen.

All settings live in the link itself (after `#o=` for the tag, `#p=` for the drops-only link). After changing anything, copy the link again.

## For TYTGEAR (brand settings)

Edit the `BRAND` block near the top of the script in `index.html`:

| Setting | What it does |
| --- | --- |
| `offer` | Discount text shown with creator codes (currently `10% OFF`) |
| `popupSeconds` | How long each product drop stays on screen |
| `firstPopupAfter` | Seconds after the overlay loads before the first drop |
| `allowedEvery` | Drop frequencies creators can choose, in minutes |
| `allowDisable` | `true` lets creators turn drops off; `false` forces drops on |
| `products` | Catalog snapshot from tytgear.in (in-stock items) |

### Product catalog

Drops rotate through every category in turn, and through every product in a category before repeating.

On load the overlay tries the live WooCommerce Store API at `tytgear.in/wp-json/wc/store/v1/products`. The store currently blocks requests from other sites (no CORS `Access-Control-Allow-Origin` header), so the overlay falls back to the snapshot in `products`. Allowing the overlay's domain in the store's CORS settings makes new products and prices appear automatically.

Product photos load from tytgear.in with `referrerpolicy="no-referrer"`, because the site's hotlink protection blocks image requests that come from other sites.

## Hosting

Turn on GitHub Pages for this repo (**Settings → Pages → Deploy from branch → main / root**) to get a public editor URL that creators can use and that OBS can load.
