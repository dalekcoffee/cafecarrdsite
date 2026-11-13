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

Store tiles with platform logos and rarity chips, grouped into "Synced inventory" and "Separate inventory" frames, plus a rarity guide. Set `--bg` at the top of the CSS to your Carrd page background. Store links, rarities and copy are near the top of the `HTML` template in `Marketplaces/embed.js`.

## Inventory

A searchable card list: "Cards in stock" with a "Checked N min ago" note, a search box (card name or card number, so `075` or `ebp01 075` finds EBP01-075), filters for colour, store and rarity, a sort menu (card number, name, colour, rarity, store, price high to low or low to high), a results box that scrolls on its own and adds cards as you near the bottom (no "Show more" button), a footnote on why prices differ between stores, and one button per store on each card with the platform logo and price. There is no checkout: each button opens that store's own page in a new tab. Card art comes from the official card art cache; if a picture does not load the card shows a plain frame.

```html
<div id="tpc-inventory" data-src="LIST_ADDRESS"></div>
<script src="https://dalekcoffee.github.io/cafecarrdsite/Inventory/embed.js"></script>
```

The list address is never stored in this repo: it is read from `data-src` on the mount div (or on the script tag) and must be `https://`. The preview page uses the sample list `Inventory/sample.json`, which has made-up prices. The list is JSON: `{"v":1,"at":<ms epoch>,"cards":[{"code","name","rarity","colour","set","stores":[{"store","cents","url"}]}]}` with stores `ebay`, `mercari`, `tcgplayer`, `cardtrader`, `cardnexus`; store links are only shown when they point at that store's own domain. Set `--bg` at the top of the CSS to your Carrd page background.

### Live rarities on the Marketplaces tiles

When the Inventory embed is on the same page, it announces which rarities each store has in stock (`window.tpcStock` and a `tpc-stock` event). The Marketplaces tiles then show those rarities instead of their fixed chips. Without the Inventory embed on the page, or if its list fails to load, the fixed chips stay. No change to either Carrd snippet is needed.

### Marketplaces in a narrow column

The Marketplaces embed sizes itself to the column it sits in, not to the screen (CSS container queries).
Above 760 px wide it is the full desktop layout; from 521 to 760 px (a hero column, for example) the tiles
stay side by side in a slim form (small logo, small chips, an arrow in the corner in place of the "Shop on" line); at 520 px
and below each store becomes one row. The rarity chips always stay on one row: their text shrinks with the
number of chips, and they only wrap when there are too many to read.

### Card list width on desktop

From 1240 px screen width the card list matches the width and position of the page section that holds the
Marketplaces embed (the widest block around it that is still narrower than the page), so both line up.
Below that it follows its own column. Without the Marketplaces embed it fills the section it sits in.

### Rarity guide

The rarity guide is one lean row at the top of the Inventory embed, above the search, and lists only the
rarities in stock. The Marketplaces embed no longer shows the big guide; add `data-guide="on"` to its
`tpc-markets` div to bring it back there.

### Fade in

Both embeds fade in the way the rest of the Carrd page does (Carrd's "On Visible" animation: Fade In, 1 s
long after a 1 s delay, not replayed). Readers who ask for reduced motion see the embeds at once.
