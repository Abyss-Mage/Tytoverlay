# TYTGEAR Overlay Studio

An animated creator name tag and TYTGEAR product drops for OBS, with a web editor. Everything is in one file, `index.html`.

## For creators

1. Open the editor (`index.html`, or the GitHub Pages URL once Pages is enabled).
2. Fill in your name and TYTGEAR creator code, then pick a finish, typeface and animations.
3. Press **Copy tag link** in the Preview row. In OBS add **Sources → + → Browser**, paste the link and use the size the editor shows (520 × 118 plus 60 px padding at default size).
4. Product drops run on their own link: press **Copy drops link** under **Product drops** and add it as a second Browser source, anywhere on screen. Creators can only enable or disable drops.

All settings live in the link itself (after `#o=` for the tag, `#p=` for the drops link). After changing anything, copy the links again.

## For TYTGEAR (brand settings)

Edit the `BRAND` block near the top of the script in `index.html`:

| Setting | What it does |
| --- | --- |
| `offer` | Discount text shown with creator codes (currently `10% OFF`) |
| `popupSeconds` | How long each product drop stays on screen |
| `firstPopupAfter` | Seconds after the overlay loads before the first drop |
| `popEvery` | Minutes between drops, the same for every creator (currently 10) |
| `allowDisable` | `true` lets creators turn drops off; `false` forces drops on |
| `products` | Catalog snapshot from tytgear.in (in-stock items) |

### Product catalog

Each drop is a slim bar the same height as the name tag, showing one product photo, the name, price and sizes, and the creator's code. Drops rotate through every category in turn, and through every product in a category before repeating.

On load the overlay tries the live WooCommerce Store API at `tytgear.in/wp-json/wc/store/v1/products`. The store currently blocks requests from other sites (no CORS `Access-Control-Allow-Origin` header), so the overlay falls back to the snapshot in `products`. Allowing the overlay's domain in the store's CORS settings makes new products and prices appear automatically.

Product photos load from tytgear.in with `referrerpolicy="no-referrer"`, because the site's hotlink protection blocks image requests that come from other sites.

## Hosting

Turn on GitHub Pages for this repo (**Settings → Pages → Deploy from branch → main / root**) to get a public editor URL that creators can use and that OBS can load.
