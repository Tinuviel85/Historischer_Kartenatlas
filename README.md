# Historischer Kartenatlas – erweiterte Version

Interaktiver, mobil nutzbarer Atlas für georeferenzierte historische Karten auf Basis von Leaflet 1.9.4. Eigenständige Weiterentwicklung von [Historische_Karten](https://github.com/Tinuviel85/Historische_Karten); das ursprüngliche Repository bleibt unverändert.

## Karten und Bedienung

- Die ursprünglichen **44 Karten-URLs** sind direkt in `index.html` enthalten.
- Historische Karte und heutige OpenStreetMap-Karte überlagern oder nebeneinander per Schieberegler vergleichen.
- Kartenbibliothek durchsuchen, nach Regionen filtern, datierte Karten über die Zeitleiste wechseln.
- Standort mit GPS und optionalem Richtungskegel; **Kartenbewegung/Zoom pausiert die automatische Zentrierung**, ohne die GPS-Aufzeichnung zu beenden. „Neu zentrieren“ aktiviert das Folgen wieder.
- Karteninformationen, Favoriten, Adresssuche und teilbare Kartenausschnitte.

## Neue Quellen hinzufügen

In der Kartenbibliothek unten auf **„＋ Neue Kartenquelle“** tippen und Typ, Name, Region und URL angeben.

| Typ | Eingabe | Technische Voraussetzungen |
| --- | --- | --- |
| XYZ | HTTPS-Kachelvorlage, z. B. `https://host/tiles/{z}/{x}/{y}.png` | Web-Mercator-Kacheln |
| WMS | HTTPS-WMS-Basis-URL und exakter Layername | EPSG:3857, WMS 1.3.0, transparente PNG-Ausgabe |
| WMTS | HTTPS-ResourceURL mit `{TileMatrix}`, `{TileCol}`, `{TileRow}` | GoogleMapsCompatible / Web Mercator, Standard-Matrixkennungen 0, 1, 2 ... |
| IIIF / Allmaps | HTTPS-URL einer **Georeference Annotation** | Bereits georeferenziert, nicht allein IIIF-`info.json`/Manifest; Kachelerzeugung über [Allmaps Tile Server](https://allmaps.org/) |

Quellen sind nur dann nutzbar, wenn der Server erreichbar ist, die Kacheln die richtige Projektion benutzen und die Einbindung erlaubt ist. Ein Rohscan ohne Georeferenzierung kann nicht direkt deckungsgleich angezeigt werden.

**Wichtig:** Über die Oberfläche neu hinzugefügte Karten werden **nur lokal im Browser** gespeichert (`localStorage`). Sie erscheinen nicht automatisch auf anderen Geräten und werden nicht in GitHub geschrieben. Für einen dauerhaften, geräteübergreifenden Kartenkatalog können Einträge später ebenfalls fest in `index.html` hinterlegt werden.

## Veröffentlichung

Statische Website, kein Build-Prozess und kein Backend erforderlich. In GitHub unter **Settings → Pages → Build and deployment → Deploy from a branch → main / (root)** auswählen.

Anschließend unter `https://tinuviel85.github.io/Historischer_Kartenatlas/` erreichbar, wenn GitHub Pages aktiviert wurde.

## Quellen und Datenschutz

Grundkarte: © OpenStreetMap-Mitwirkende. Historische Karten stammen von den verknüpften Drittanbietern; deren Quellenangaben, Lizenzbedingungen und Nutzungsrichtlinien gelten. Die Allmaps-Erweiterung nutzt einen externen Kachelserver. Standortabfragen erfolgen erst nach Zustimmung des Nutzers. Die App versendet keine GPS-Koordinaten an ein eigenes Backend; externe Karten- und Suchdienste erhalten die für die Abfrage notwendigen Karten- bzw. Suchparameter.

## Technische Grenzen

- WMS-/WMTS-Dienste außerhalb EPSG:3857/GoogleMapsCompatible erfordern zusätzliche Projektionslogik.
- Nicht verfügbare Kartenserver werden nicht durch die Anwendung ersetzt.
- Die Kompassrichtung ist auf Smartphones von Browser- und Sensorberechtigungen abhängig.
- Für alle neuen Karteneinträge müssen räumliche Abdeckung und Nutzungsrechte überprüft werden.
