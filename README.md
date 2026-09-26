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

## Data ja synkronointi

Mittaukset ovat yksityisessä repossa `wessmanjere/kasvikaksonen-data` tiedostossa `data.json`. Sivu on julkinen, data ei.

- Laite, jolle on yhdistetty GitHub-avain, lukee datan GitHubista ja jokainen tallennus tekee commitin datarepoon. Puhelin ja tietokone näkevät samat tiedot.
- Ilman avainta sivu on lukutilassa: kasvit näkyvät, mittauksia ei näy eikä mitään voi muuttaa.
- Muutokset menevät ensin laitteen jonoon, joten tallennus toimii myös ilman verkkoa ja lähtee, kun yhteys palaa. Jos kaksi laitetta tallentaa yhtä aikaa, sivu hakee uusimman version ja ajaa omat muutokset sen päälle.

### Avaimen luonti (kerran per laite)

1. Avaa https://github.com/settings/personal-access-tokens/new
2. Token name esim. `Kasvikaksonen puhelin`, Expiration esim. 1 vuosi.
3. Repository access: Only select repositories, valitse `kasvikaksonen-data`.
4. Repository permissions: Contents, Read and write.
5. Generate token, kopioi avain ja liitä se sivulla kohtaan Lukutila / Synkronointi.

Avain tallentuu vain kyseisen laitteen selaimeen. Kadonneen puhelimen avaimen voi perua GitHubissa samalta sivulta.

## Käyttö

Avaa `index.html` selaimessa tai julkaise GitHub Pagesissa:

1. Settings → Pages → Source: Deploy from a branch, branch `main`, folder `/ (root)`.
2. Sivu löytyy osoitteesta `https://<käyttäjä>.github.io/<repo>/`.

## Rakenne

Kaikki on `index.html`-tiedostossa kolmessa script-lohkossa:

1. **Data ja säännöt**: `SPECIES` (lajien tavoitearvot), `FLOORS`, `PLANTS`, `score()`, `visualState()`, `trend()`, `suggestions()`.
2. **Kasvikuvat**: `ART[laji](id, state)` piirtää SVG:n. Uusi laji lisätään tänne ja `SPECIES`-tauluun.
3. **Käyttöliittymä**: renderöinti, laatikko (lomake, historia, kaaviot, tavoitearvot), vienti, GitHub-synkronointi (`sync()`, `commit()`, `applyOp()`), teema.

`store.v` on localStorage-välimuistin skeeman versio. Kun datamalli muuttuu, lisää askel `migrate()`-funktioon.

## Claude-artefaktin lisäominaisuudet

Sivu tunnistaa ajoympäristön. Claude.ai-artefaktina se käyttää `sample`-kykyä (tekoälykysymykset kasvista) ja `downloads`-kykyä. GitHub Pagesissa tekoälykortti piilotetaan ja lataus tapahtuu tavallisena selainlatauksena.

## Lisenssi

MIT
