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

A searchable card list: "Cards in stock" with a "Checked N min ago" note, a search box (card name or card number, so `075` or `ebp01 075` finds EBP01-075), filters for colour, store and rarity, a sort menu (card number, name, colour, rarity, store, price high to low or low to high), 24 cards per page with "Show more", and one button per store on each card with the platform logo and price. There is no checkout: each button opens that store's own page in a new tab. Card art comes from the official card art cache; if a picture does not load the card shows a plain frame.

```html
<div id="tpc-inventory" data-src="LIST_ADDRESS"></div>
<script src="https://dalekcoffee.github.io/cafecarrdsite/Inventory/embed.js"></script>
```

The list address is never stored in this repo: it is read from `data-src` on the mount div (or on the script tag) and must be `https://`. The preview page uses the sample list `Inventory/sample.json`, which has made-up prices. The list is JSON: `{"v":1,"at":<ms epoch>,"cards":[{"code","name","rarity","colour","set","stores":[{"store","cents","url"}]}]}` with stores `ebay`, `mercari`, `tcgplayer`, `cardtrader`, `cardnexus`; store links are only shown when they point at that store's own domain. Set `--bg` at the top of the CSS to your Carrd page background.
