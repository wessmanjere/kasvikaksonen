# Kasvikaksonen

Kodin kasvien digitaalinen kaksonen. Yksi html-tiedosto, ei build-vaihetta, ei riippuvuuksia. Toimii puhelimella ja tietokoneella, tumma ja vaalea teema.

## Mitä se tekee

- Näyttää kasvit kerroksittain (3. kerros, 2. kerros, alakerta huoneineen, ulkona) proseduraalisina SVG-kuvina. Kasvin ulkonäkö reagoi kuntoon: kuiva multa nuokuttaa lehtiä ja ruskettaa reunat, pH-poikkeama kellastaa, viileä harmaannuttaa.
- Mittausten syöttö per kasvi: päivämäärä, mullan pH, lämpötila, kosteus (kuiva / ok / märkä) ja toimenpiteet (kasteltu, lannoitettu, vaihdettu multa, siirretty).
- Kuntoindeksi 0–100 lajikohtaisiin tavoitearvoihin verrattuna. Laskukaava näkyy kasvin kortilla.
- Tänään-lista sääntöpohjaisista ehdotuksista (kastelu, lannoitus, siirto sisälle, happamoituvat mullat, sopeutumisaika siirron jälkeen). Jokaisen ehdotuksen sääntö näytetään.
- Trendit ja ennusteet pH:lle ja lämpötilalle, kaaviot per kasvi, vuodenajan huomiointi (Tampereen talvi hidastaa kasvua).
- Tavoitearvot muokattavat per kasvi.
- Vienti CSV (puolipiste, Excel) ja JSON, tuonti JSON.

Data tallentuu selaimen localStorageen. Laitteiden välillä data siirtyy JSON-viennillä ja -tuonnilla.

## Käyttö

Avaa `index.html` selaimessa tai julkaise GitHub Pagesissa:

1. Settings → Pages → Source: Deploy from a branch, branch `main`, folder `/ (root)`.
2. Sivu löytyy osoitteesta `https://<käyttäjä>.github.io/<repo>/`.

## Rakenne

Kaikki on `index.html`-tiedostossa kolmessa script-lohkossa:

1. **Data ja säännöt**: `SPECIES` (lajien tavoitearvot), `FLOORS`, `PLANTS`, `SEED` (lähtömittaukset 26.9.2026), `score()`, `visualState()`, `trend()`, `suggestions()`.
2. **Kasvikuvat**: `ART[laji](id, state)` piirtää SVG:n. Uusi laji lisätään tänne ja `SPECIES`-tauluun.
3. **Käyttöliittymä**: renderöinti, laatikko (lomake, historia, kaaviot, tavoitearvot), vienti, teema.

`store.v` on localStorage-skeeman versio. Kun datamalli muuttuu, lisää askel `migrate()`-funktioon.

## Claude-artefaktin lisäominaisuudet

Sivu tunnistaa ajoympäristön. Claude.ai-artefaktina se käyttää `sample`-kykyä (tekoälykysymykset kasvista) ja `downloads`-kykyä. GitHub Pagesissa tekoälykortti piilotetaan ja lataus tapahtuu tavallisena selainlatauksena.

## Lisenssi

MIT
