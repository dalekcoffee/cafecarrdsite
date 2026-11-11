# cafecarrdsite

Embeds for the ThePalCafe Carrd site, served with GitHub Pages. Each embed lives in its own folder with an `embed.js` and an `index.html` preview page.

| Embed | Preview | Script |
|---|---|---|
| Marketplaces | [Marketplaces/](https://dalekcoffee.github.io/cafecarrdsite/Marketplaces/) | `https://dalekcoffee.github.io/cafecarrdsite/Marketplaces/embed.js` |

## Using an embed in Carrd

Add an **Embed** element (Type: Code) and paste:

```html
<div id="tpc-markets"></div>
<script src="https://dalekcoffee.github.io/cafecarrdsite/Marketplaces/embed.js"></script>
```

## Marketplaces

Store tiles with platform logos and rarity chips, grouped into "Synced inventory" and "Separate inventory" frames, plus a rarity guide. Set `--bg` at the top of the CSS to your Carrd page background. Store links, rarities and copy are near the top of the `HTML` template in `Marketplaces/embed.js`.
