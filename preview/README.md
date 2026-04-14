# Preview

Lokale Vorschau der Jekyll-Seite per Docker.

## Starten

```bash
cd preview
docker compose up
```

Die Seite ist dann erreichbar unter: **http://localhost:4000**

Änderungen an Dateien werden automatisch erkannt und die Seite wird neu generiert (LiveReload auf Port 35729).

## Wann `--build` nötig ist

```bash
docker compose up --build
```

Ein Rebuild des Images ist nötig, wenn sich die **Gemfile** oder **Gemfile.lock** geändert haben,
z.B. nach dem Hinzufügen, Entfernen oder Aktualisieren von Gems.
Bei reinen Änderungen an Inhalten, Layouts oder CSS reicht ein normales `docker compose up`.

## Was das Dockerfile baut

Das Dockerfile erzeugt ein Image auf Basis von **Ruby 3.3** (slim) und installiert darin
die im Gemfile definierten Ruby-Gems (Jekyll und alle Abhängigkeiten) per `bundle install`.

Das eigentliche Projektverzeichnis wird zur Laufzeit per Volume eingebunden (`..:/site`),
sodass Jekyll direkt auf die aktuellen Quelldateien zugreift.
Die Gems selbst sind im Image gecacht – deshalb muss bei Gemfile-Änderungen neu gebaut werden.

## Stoppen

```bash
docker compose down
```

