# Vignale Gamine - historische dossiers (site)

Kleine statische site met per Gamine een historisch dossier: kerngegevens uit de
overzichtssheet, plus wat er in openbare bronnen (veilinghuizen, vignalegamine.net,
openbare registratiedata) over die specifieke auto te vinden is.

Opgezet 2026-08-31 op verzoek van Frank, om met Martin te delen.

## Waar het staat

- **Bron (canoniek):** deze map (`projecten/Vignale-Gamine/dossier-site/`).
- **GitHub:** publieke repo `mixe66/vg-636d5603` (bewust cryptische naam).
- **Live:** https://mixe66.github.io/vg-636d5603/ (GitHub Pages, branch `main`, root).

## Inhoud

- `<chassis>.html` - 21 dossiers voor de auto's met echte veiling-/herkomsthistorie
  (uit de webresearch van 31-08-2026), plus `1911571.html` ("The Flying Vignale").
- De 20 worden gegenereerd; `1911571.html` is met de hand gemaakt.
- **Geen `index.html`.** De dossiers zijn alleen bereikbaar via de chassisnummer-links
  in de overzichtssheet (kolom B). De root-URL geeft een 404.

## Afscherming

Geen echte toegangscontrole (kan alleen met GitHub Enterprise). In plaats daarvan:

- repo-naam is niet te raden;
- `<meta name="robots" content="noindex, nofollow">` op elke pagina;
- `robots.txt` met `Disallow: /`.

De dossiers bevatten de eigenaarsvoornaam en het motornummer uit de sheet, die
bewust niet op vignalegamine.net staan. Link alleen binnen de club delen.

## Bijwerken (de 20 gegenereerde dossiers)

1. Pas de feiten aan in `overig/scripts/vignale-gamine-analyse/dossier_teksten.py`
   (narratief) en/of ververs `_dossier_rows.json` (kerngegevens uit de sheet).
2. `python3 overig/scripts/vignale-gamine-analyse/bouw_dossiers.py`
   -> schrijft naar deze map. `1911571.html` wordt bewust overgeslagen; een
   eventuele oude `index.html` wordt verwijderd.
3. Deploy:
   ```
   git clone https://github.com/mixe66/vg-636d5603 && cd vg-636d5603
   cp <repo>/projecten/Vignale-Gamine/dossier-site/*.html . && \
     cp <repo>/projecten/Vignale-Gamine/dossier-site/{robots.txt,.nojekyll} . && \
     git rm --ignore-unmatch index.html && \
     git add -A && git commit -m "..." && git push
   ```
4. Pages herbouwt automatisch (~1 min).

## Link vanuit de overzichtssheet

Tab "Alle Gamines", kolom B (VIN): op de 21 dossierauto's is een rich-text
hyperlink op de chassisnummer-tekst gezet naar
`https://mixe66.github.io/vg-636d5603/<chassis>.html`. Geen aparte kolom, geen
`=HYPERLINK`-formule (de cel-waarde blijft de kale string, zodat Martins
draaitabellen ongemoeid blijven).
