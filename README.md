# Heizkosten-Rechner für zwei Wohnungen (EG/OG) mit zentraler Gasheizung

Ein einfaches, lokales Web-Tool zur transparenten, fairen und rechtlich korrekten Abrechnung von Heiz-, Warmwasser-, Frischwasser-, Abwasser- und Stromkosten zwischen zwei gleich großen Wohnungen, die eine gemeinsame Gasheizung nutzen.

## Funktionsweise & Berechnungslogik

### Gas/Heizkosten (nach Heizkostenverordnung)
- Gesamte Gaskosten werden auf die abgegebene Wärme (Raumheizung + Warmwasser) umgelegt → €/kWh
- **Raumheizung**: 30 % Grundkosten (50/50 nach Wohnfläche) + 70 % verbrauchsabhängig (nach Wärmemengenzähler kWh EG/OG)
- **Warmwasser**: 30 % Grundkosten (50/50) + 70 % verbrauchsabhängig (nach Warmwassermengenzähler m³ EG/OG)
- Der Vermieter legt diese Kosten auf die Mieter um.

### Frischwasser (Kaltwasser für Warmwasserbereitung + evtl. Nachfüllung)
- Gesamtmenge aus Zwischenzähler (m³)
- Der Teil, der dem gemessenen Warmwasserverbrauch (Summe m³ EG + OG) entspricht → **verbrauchsabhängig** nach m³ aufteilen
- Differenz (z. B. Nachfüllung des Heizkreises) → **50/50** geteilt
- EG zahlt zunächst alles → OG erstattet seinen Anteil

### Abwasser
- Basierend auf der **gesamten bezogenen Frischwassermenge** (Zwischenzähler)
- Aufteilung **proportional zum Frischwasseranteil** jeder Wohnung (berücksichtigt bereits verbrauchsabhängigen Teil + 50/50-Differenz)
- EG zahlt zunächst → OG erstattet seinen Anteil

### Strom (Allgemeinstrom inkl. Heizung)
- Eingabe: **Gesamter Zählerstand** (inkl. Heizung) + separater Heizungsstrom (aus Heizungs-App)
- Heizungsstrom wird abgezogen → Kosten verbrauchsabhängig verteilt (proportional zur gelieferten Wärme: Heizkreis + anteiliger Warmwasseranteil)
- Restlicher Allgemeinstrom (ohne Heizung) → **50/50** geteilt
- EG zahlt zunächst alles → OG erstattet seinen Anteil

### Zusammenfassung
- Klare Tabelle: Was jeder an den Vermieter zahlt (Gasumlage) und wie viel das OG dem EG erstatten muss (Wasser + Strom)

## Besonderheiten
- Alle Berechnungen mit detaillierten Zwischenwerten in den Tabellen für maximale Nachvollziehbarkeit
- Daten können im Browser (LocalStorage) gespeichert und gelöscht werden
- Keine externen Abhängigkeiten – läuft komplett offline
- Schönes, responsives Layout mit harmonischen Buttons und Sections

## Verwendung
1. `index.html` herunterladen oder kopieren
2. Im Browser öffnen (einfach per Doppelklick)
3. Alle Zählerstände und Preise eingeben
4. „Berechnen“ klicken
5. Ergebnisse ablesen und bei Bedarf speichern

## Vollständiger Prompt (zur Reproduktion)
Falls du das Tool später neu generieren möchtest, hier der komplette Prompt, der diesen exakten Rechner erzeugt:
> Zwei Wohnungen (EG und OG) teilen sich neuerdings eine zentrale Gasheizung. Erstelle mir eine HTML Javascript Website mit wenig Abhängigkeiten, damit die angefallenen Kosten fair und rechtlich korrekt verteilt werden. Die Berechnung sollte in übersichtlichen Tabellen dargestellt werden. Beachte dabei auch die Heizkostenverordnung bzw. die 30/70 Regel. Dies gilt für Heizung und auch für Warmwasser. Die Wohnungen sind beide etwa 78 qm groß und sonst identisch aufgebaut. Die Heizung befindet sich selbst im OG. Es existieren folgende Zähler: Warmwasser (m³) für EG, Warmwasser (m³) für OG, Wärmemengenzähler Heizkreis EG (kWh), Wärmemengenzähler Heizkreis OG (kWh), Wärmemengenzähler Warmwasser (kWh) gesamt. Gegeben seien die angefallenen Gaskosten, die verteilt werden müssen. Außerdem gibt folgende Sonderfälle: 1. Das Kaltwasser für die Heizung (was später Warmwasser für beide Wohnungen wird) geht vom Wasserzähler des EG ab. Hierfür gibt es noch einen separaten Zwischenzähler. Die Kosten müssen hier also ebenfalls aufgeteilt werden, bzw. muss das OG dem EG erstatten. Beachte, dass auch das Abwasser fair geteilt werden muss, da auch dies das EG erst einmal zahlt. Dieses hat einen unterschiedlichen Preis zum Frischwasser. Das Abwasser entspricht der gesamten bezogenen Frischwassermenge (Zwischenzähler). Für das Frischwasser: Der Teil, der dem Warmwasserverbrauch (Summe m³ EG + OG) entspricht, wird verbrauchsabhängig nach m³ aufgeteilt. Die Differenz (z.B. Nachfüllung Heizkreis) wird 50/50 geteilt. 2. Ähnliches Szenario für den Allgemeinstrom, auch hier ist die Heizung angeschlossen und es läuft technisch über den Zähler des EG. Der Allgemeinstromzähler beinhaltet auch den Heizungsstrom. In den Rechner soll man also wirklich den gesamten Zählerstand eingeben. Dennoch gibt es das weitere Feld für den Heizungsstrom, was man von der App abliest. Es soll auf der Oberfläche bzw. im Ergebnis erkennbar sein, dass bei der Berechnung des Allgemeinstroms der Heizungsstrom abgezogen wurde. Anschließend der Allgemeinstromrest halbieren (50/50), der Heizungsstrom verbrauchsabhängig machen (proportional zur gelieferten Wärme: Heizkreis + anteiliger Warmwasseranteil). Der Vermieter zahlt das Gas, auf ihm ist der Zähler angemeldet. Wasser und Strom übernimmt zunächst das EG. Bitte am Ende in einer Tabelle zusammenfassen, wer jetzt wie viel bezahlen muss und wie die Erstattung aussieht. Die eingegebenen Werte sollen auf Wunsch in den LocalStorage gespeichert werden (Button). Es soll auch einen Button geben, um alle Werte aus dem LocalStorage wieder zu entfernen. Aus den Tabellen soll auch die Verteilung 30:70 hervorgehen, damit man die Berechnung nachvollziehen kann. In den Ergebnistabellen neben den Eurowerten auch die (Zwischen)werte angeben, sonst lässt sich das nicht so leicht nachvollziehen. Der "Berechnen"-Button soll optisch bündig zu den Eingabefeldern sein (gleiche Breite, gutes Padding, harmonisches Layout). Die Sections sollen einen leichten Hintergrund und abgerundete Ecken haben. In der Stromtabelle soll die Zeile "Allgemeinstrom (Zählerstand gesamt)" heißen und den gesamten Verbrauch zeigen, darunter eingerückt "davon Heizungsstrom (abgezogen)" und "davon Rest-Allgemeinstrom". Abwasser soll einfach "Abwasser" heißen.
