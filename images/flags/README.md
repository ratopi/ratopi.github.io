# Flag Icons

Minimale SVG-Flaggen für die Sprachumschaltung im Blog.

## Herkunft

Die SVGs sind **selbst erstellt** nach den offiziellen Farbwerten und Proportionen der jeweiligen Nationalflaggen. Keine externen Abhängigkeiten.

## Vorhandene Flaggen

| Datei    | Sprache  | Verwendung im Front Matter |
|----------|----------|----------------------------|
| `de.svg` | Deutsch  | `lang: de`                 |
| `gb.svg` | Englisch | `lang: en`                 |

## Neue Sprache hinzufügen

1. SVG-Datei hier ablegen, Dateiname = Ländercode (z.B. `fr.svg`, `es.svg`, `nl.svg`).
2. In `_layouts/blog_post.html` ein `{% elsif %}` ergänzen, z.B.:
   ```liquid
   {% elsif p.lang == "fr" %}{% assign flag_code = "fr" %}{% assign flag_text = "Français" %}
   ```
3. In beiden Partner-Posts das Front Matter setzen:
   ```yaml
   lang: fr
   lang_partner: 2026-04-14-titel-des-partner-posts
   ```

## SVG-Quellen & Farbwerte

### Deutschland (`de.svg`)
- Proportionen: 5:3
- Schwarz: `#000000`
- Rot: `#DD0000`
- Gold: `#FFCE00`

### Vereinigtes Königreich (`gb.svg`)
- Proportionen: 2:1
- Blau: `#012169`
- Rot: `#C8102E`
- Weiß: `#FFFFFF`

### Weitere Referenzen
- Wikipedia: [Gallery of sovereign state flags](https://en.wikipedia.org/wiki/Gallery_of_sovereign_state_flags)
- Offizielle Farbwerte: [Flags of the World (FOTW)](https://www.crwflags.com/fotw/flags/)

