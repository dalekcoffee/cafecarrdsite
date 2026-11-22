# cafecarrdsite

Embeds for the ThePalCafe Carrd site, served with GitHub Pages. Each embed lives in its own folder with an `embed.js` and an `index.html` preview page.

| Embed | Preview | Script |
|---|---|---|
| Marketplaces | [Marketplaces/](https://dalekcoffee.github.io/cafecarrdsite/Marketplaces/) | `https://dalekcoffee.github.io/cafecarrdsite/Marketplaces/embed.js` |
| Inventory | [Inventory/](https://dalekcoffee.github.io/cafecarrdsite/Inventory/) | `https://dalekcoffee.github.io/cafecarrdsite/Inventory/embed.js` |

## Using an embed in Carrd

Add an **Embed** element (Type: Code) and paste:

```html
<div id="tpc-markets"></div>
<script src="https://dalekcoffee.github.io/cafecarrdsite/Marketplaces/embed.js"></script>
```

## Marketplaces

Store tiles with platform logos and rarity chips, in two rows (Mercari, eBay; then CardTrader, CardNexus, TCGplayer), with no synced or separate headings, plus an optional rarity guide. Set `--bg` at the top of the CSS to your Carrd page background. Store links, rarities and copy are near the top of the `HTML` template in `Marketplaces/embed.js`.

## Inventory

A searchable card list: "Cards in stock" with a "Checked N min ago" note, a search box (card name or card number, so `075` or `ebp01 075` finds EBP01-075), filters for color, set, store and rarity, a sort menu (card number, name, color, set, rarity, store, price high to low or low to high), a results box that scrolls on its own and adds cards as you near the bottom (no "Show more" button), a footnote on why prices differ between stores, a **Sealed product** tab when sealed product is in stock (see Sealed product below), and one button per store on each card with the platform logo and price. There is no checkout: each button opens that store's own page in a new tab. Card art comes from the official card art cache; if a picture does not load the card shows a plain frame.

```html
<div id="tpc-inventory" data-src="LIST_ADDRESS"></div>
<script src="https://dalekcoffee.github.io/cafecarrdsite/Inventory/embed.js"></script>
```

The list address is never stored in this repo: it is read from `data-src` on the mount div (or on the script tag) and must be `https://`. The preview page uses the sample list `Inventory/sample.json`, which has made-up prices. The list is JSON: `{"v":1,"at":<ms epoch>,"cards":[{"code","name","rarity","colour","set","stores":[{"store","cents","url"}]}]}` with stores `ebay`, `mercari`, `tcgplayer`, `cardtrader`, `cardnexus`; store links are only shown when they point at that store's own domain. Set `--bg` at the top of the CSS to your Carrd page background.

### Sealed product

When the list has a `sealed` part (boxes, trial decks, booster packs and promo packs in stock), the Inventory embed gets two tabs, **Cards** and **Sealed product**; with only one of them in stock there are no tabs. The sealed tab has the same look as the cards: a search box (name, type or set), filters for **set** (the human set code, EBP01, ETD01), **type** (booster box, trial deck, booster pack, promo pack), **weight** and **store**, a sort menu (set, type, weight light to heavy or heavy to light, name, store, price) and the same store buttons and zoom view. A weighed pack shows its weight as "approx. 15.32 g"; the weight filter has whole-gram steps built from the weights in stock (at most six) and "Weight not listed", and the weight filter and sorts are left out when no weight is listed. Products with no weight sort after the weighed ones. The picture is the product picture on TCGplayer's own image host (`SEALED_ART` at the top of `Inventory/embed.js`); when it does not load the tile keeps a plain frame with the product type in words. The list format: `"sealed":[{"product":<TCGplayer product number>,"name","kind":"box"|"deck"|"pack"|"promo","set":"EBP01","grams":15.32,"stores":[{"store","cents","url"}]}]` (`grams` only on a weighed pack). The sample list has made-up sealed products.

### Live rarities on the Marketplaces tiles

When the Inventory embed is on the same page, it announces which rarities each store has in stock (`window.tpcStock` and a `tpc-stock` event). The Marketplaces tiles then show those rarities instead of their fixed chips. Without the Inventory embed on the page, or if its list fails to load, the fixed chips stay. No change to either Carrd snippet is needed.

### Marketplaces in a narrow column

The Marketplaces embed sizes itself to the column it sits in, not to the screen (CSS container queries).
Above 760 px wide it is the full desktop layout; from 521 to 760 px (a hero column, for example) the tiles
stay side by side in a slim form (small logo, small chips, an arrow in the corner in place of the "Shop on" line); at 520 px
and below each store becomes one row. The rarity chips always stay on one row: their text shrinks with the
number of chips, and they only wrap when there are too many to read.

### Card list width on desktop

From 737 px screen width (above phone size) the card list lines up with the row that holds the Marketplaces embed, from the left
edge of that row's content to the right edge of what sits beside it (a logo for example). Below that it follows
its own column, and without the Marketplaces embed on the page it keeps its own column too.

### Rarity guide

The rarity guide is one lean row at the top of the Inventory embed, above the search, and lists only the
rarities in stock. The Marketplaces embed no longer shows the big guide; add `data-guide="on"` to its
`tpc-markets` div to bring it back there.

### Fade in

Both embeds fade in the way the rest of the Carrd page does (Carrd's "On Visible" animation: Fade In, 1 s
long after a 1 s delay, not replayed). Readers who ask for reduced motion see the embeds at once.

### Zoom view

Each card in the Inventory list opens an enlarged view when you click it (or focus it and press Enter or Space): a bigger picture, the card number, rarity tag, name, color and set, and the same store buttons at a larger size. The store buttons on the card still go straight to the store in a new tab and never open the zoom. Close it with the × button, a click outside, or Esc; focus returns to the card. The picture uses the same official art through the proxy (ESOUL name first).

### Rarity order and the SSS tag

The Inventory list opens sorted by rarity, highest first: SSS, TSP, SSP, SP, OSR / TSR, SR, RR, PR, R, U, C, TD / S (the order of PalVault's rarity floors). The sort menu still changes it. SSS has a gold foil tag whose shine drifts and whose glow pulses; for readers who ask for reduced motion it stays still. No change to either Carrd snippet is needed: the embeds load `embed.js` from GitHub Pages, and browsers may keep the old script for about 10 minutes after the merge.
