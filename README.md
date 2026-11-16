# blueplant-docs

Endkunden-Dokumentation („Product Guide") für **blueplant** — die Software für
professionelle Innenraumbegrünung.

Live: **[docs.blueplant.cloud](https://docs.blueplant.cloud)** · Website: [blueplant.cloud](https://blueplant.cloud)

Gebaut mit **[Mintlify](https://mintlify.com)**: MDX-Seiten mit YAML-Frontmatter,
Navigation und Theme in `docs.json`. Kein Build-Schritt im Repo, kein `package.json`.

## Struktur

| Ordner | Inhalt |
| --- | --- |
| `erste-schritte/` | Einstieg und Grundbegriffe |
| `buero/` | Web-CRM: Arbeit im Büro |
| `unterwegs/` | Mobile-App: Arbeit beim Kunden |
| `wissenswertes/` | Tarife, Support, Hintergrundwissen |
| `api/` | Externe API |
| `changelog.mdx` | Neuerungen je Release |
| `images/<bereich>/` | Screenshots, nur aus dem Demo-Mandanten |

## Lokale Vorschau

```bash
npm i -g mint
mint dev             # http://localhost:3000
mint broken-links    # Links prüfen
```

## Deploy

Mintlify ist über seine GitHub-App mit diesem Repo verbunden. Es gibt keine eigene
CI-Pipeline.

1. **Pull Request:** Mintlify baut eine Vorschau und meldet sie als Check am PR
   (Status plus Preview-URL). Vor dem Merge abwarten und die betroffenen Seiten dort
   öffnen.
2. **Merge auf `main`:** Mintlify deployt automatisch auf `docs.blueplant.cloud`.
   Nie direkt auf `main` pushen, immer über Branch `docs/<thema>` und PR.

### Fallstricke

- **Fehlerhafte Seiten werden still übersprungen.** Ein gerades `"` in einem
  JSX-Attribut (`title=`, `caption=`, `alt=`) bricht das Parsen der Seite. Der Deploy
  meldet trotzdem `success`, die Seite liefert 404 und fehlt in `/sitemap.xml`.
  In Attributen typografische Quotes `„…“` verwenden.
- **Bilder aus einem fehlgeschlagenen Deploy werden nie nachgeladen.** Bilder und
  neues MDX deshalb in getrennten PRs ausliefern: erst die Bilder, dann den Text.
- **Live prüfen gegen `docs.blueplant.cloud`**, nicht gegen `*.mintlify.app`.

Diagnose und Hintergründe: `tools/mintlify.md` im PO-Hub (`blueplant-product-owner`).

## Inhalte schreiben

- **Ansprache:** durchgängig `du` (klein), wie Website und App.
- **Fachbegriffe** wie in der App und im Web-CRM. Beschriftungen der App vorher gegen
  `blueplant-app/assets/translations/de.json` prüfen.
- **Keine echten Kundendaten:** Screenshots nur aus dem Demo-Mandanten
  (`test.blueplant.app`).
