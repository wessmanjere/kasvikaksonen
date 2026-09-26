# Kasvikaksonen

Yksitiedostoinen html-sovellus (`index.html`), ei build-vaihetta. Kieli suomi. Älä käytä ajatusviivaa missään tekstissä (ei "–" eikä "—"), käytä pilkkua tai pistettä.

## Reunaehdot
- Kaikki yhdessä tiedostossa. Ei ulkoisia kuvia. Kirjastoja vain cdnjs.cloudflare.com kautta, tällä hetkellä ei yhtään.
- Fontit Google Fontsista (Fraunces, Public Sans), fallback-stack pakollinen.
- Teemat: tokenit `:root`-lohkossa, tumma sekä `prefers-color-scheme` että `[data-theme="dark"]` kautta. Älä määrittele väriä vain toisessa teemassa.
- Responsiivinen 400 px asti. Ei vaakascrollia.
- Kaikki `localStorage`-kutsut try/catchissa. Skeemamuutokset `migrate()`-funktioon ja `store.v` kasvatetaan.
- Sivun pitää toimia sekä claude.ai-artefaktina (`window.claude.use`) että tavallisena sivuna. Tarkista `sampleNs`/`downloadsNs` null-arvot.

## Testaus
`node -e` syntaksitarkistus script-lohkoille tai avaa `index.html` selaimessa. Playwright-kuvakaappaus: `npx playwright screenshot index.html shot.png --full-page`.

## Data
Mittaukset ovat yksityisessä repossa `wessmanjere/kasvikaksonen-data` (`data.json`), ei tässä julkisessa repossa. Älä lisää mittausdataa `index.html`-tiedostoon. Kaikki muutokset kulkevat `commit(op)` kautta: `applyOp()` ajaa saman operaation paikallisesti ja GitHubin versioon, `store.pending` on lähetysjono. Uusi muutostyyppi lisätään `applyOp()`-funktioon. Kasvien sijainnit `PLANTS`-taulussa, koko `size: "s" | "l"`.
