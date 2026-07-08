# Balaitous - Vignemale web map

Mappa statica pronta per GitHub Pages. Usa Leaflet, basemap OpenStreetMap/OpenTopoMap e layer GeoJSON generati dai GeoPackage originali.

## Aggiornare i dati

Dal workspace:

```powershell
python work\convert_gpkg_to_geojson.py
```

Lo script usa:

```text
C:\OSGeo4W\bin\ogr2ogr.exe
```

Lo script legge i GeoPackage da:

```text
D:\Maps\Commissioni\Pyrenees\Balaitous-Vignemale\data
```

Il layer `area1` viene letto da:

```text
D:\Maps\Commissioni\Pyrenees\Balaitous-Vignemale\area1.gpkg
```

Il layer `main_peak` viene letto da:

```text
D:\Maps\Commissioni\Pyrenees\data\main-peak.gpkg
```

e scrive i file in:

```text
outputs\webmap\data
```

Nota tecnica: i GeoPackage sono in `EPSG:25830`; `ogr2ogr` li riproietta in `EPSG:4326` con output GeoJSON RFC 7946, adatto a Leaflet.

## Provare in locale

Da `outputs\webmap`:

```powershell
python -m http.server 8000
```

Poi aprire:

```text
http://localhost:8000
```

Aprire direttamente `index.html` da disco puo' non funzionare perche' il browser blocca il caricamento dei GeoJSON locali via `fetch`.

## Pubblicare su GitHub Pages

1. Crea un repository GitHub.
2. Copia il contenuto di `outputs\webmap` nella root del repository, oppure nella cartella `docs`.
3. In GitHub vai su `Settings > Pages`.
4. Imposta la sorgente su `main` e scegli `/root` oppure `/docs`, coerentemente con dove hai copiato i file.
5. Condividi l'URL generato da GitHub Pages.

## Limiti

I file pubblicati su GitHub Pages sono pubblici. Non usare questa soluzione per dati riservati senza una strategia di accesso separata.
