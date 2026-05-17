# Heizkosten- und Nebenkostenrechner EG/OG

Eine eigenstaendige HTML/CSS/JavaScript-Seite zur fairen Aufteilung von Gas-, CO2-, Wasser-, Abwasser- und Stromkosten zwischen zwei Wohnungen: EG und OG.

Der Rechner ist fuer ein Zweifamilienhaus-Szenario gedacht, in dem beide Wohnungen eine zentrale Gasheizung teilen. Der Vermieter zahlt zunaechst die Gasrechnung, das EG zahlt zunaechst Wasser/Abwasser und Allgemeinstrom. Am Ende werden die Kosten und Erstattungen tabellarisch nachvollziehbar aufgeschluesselt.

## Datei

- `heizkosten-rechner.html`: komplette Anwendung als einzelne statische HTML-Datei

Die Seite benoetigt keinen Build-Prozess und keine externen Frameworks.

## Nutzung

Die Datei `heizkosten-rechner.html` direkt im Browser oeffnen oder ueber einen kleinen lokalen Webserver starten:

```bash
python -m http.server 8123 --bind 127.0.0.1
```

Danach im Browser oeffnen:

```text
http://127.0.0.1:8123/heizkosten-rechner.html
```

## Funktionen

- Verteilung der bereinigten Gaskosten nach Heizkostenverordnung mit 30/70-Regel
- Separate Behandlung der in der Gasrechnung ausgewiesenen CO2-Kosten
- CO2-Kostenaufteilung nach CO2-Kostenaufteilungsgesetz
- Verrechnung von Gas-Vorauszahlungen fuer EG und OG
- Wasser-/Abwasser-Sonderfall, wenn das Kaltwasser fuer Warmwasser/Heizung ueber den EG-Zaehler laeuft
- Strom-Sonderfall, wenn Allgemeinstrom und Heizungsstrom ueber den EG-Zaehler laufen
- Ergebnisdarstellung in nachvollziehbaren Tabellen mit Zwischenwerten
- Speichern und Loeschen der Eingabewerte im LocalStorage

## Berechnungslogik Kurzfassung

Die eingegebenen Gaskosten enthalten die CO2-Kosten. Der Rechner zieht die explizit ausgewiesenen CO2-Kosten zuerst ab. Nur die bereinigten Gaskosten werden anschliessend auf Heizung und Warmwasser verteilt.

Die bereinigten Gaskosten werden anhand der gemessenen Waermemengen in Kostenblock Heizung und Kostenblock Warmwasser aufgeteilt. Innerhalb jedes Blocks gilt:

- 30 Prozent Grundkosten nach Wohnflaeche
- 70 Prozent Verbrauchskosten

Bei Heizung laufen die Verbrauchskosten ueber die Heizkreis-Waermemengenzaehler. Bei Warmwasser laufen sie ueber die Warmwasserzaehler in m3.

Die CO2-Kosten werden separat nach CO2KostAufG auf Vermieter und Mieterseite verteilt. Der Mieterseitenanteil wird verbrauchsabhaengig auf EG und OG verteilt.

## Rechtlicher Hinweis

Der Rechner bildet die beschriebene Abrechnungslogik praxisnah ab, ersetzt aber keine Rechts- oder Steuerberatung. Vertragsdetails, Eichfristen, Betriebskostenvereinbarungen, lokale Gebuehrenbescheide und Sonderregelungen sollten gesondert geprueft werden.

## Wiederherstellungs-Prompt

Mit folgendem Prompt kann die Anwendung spaeter erneut erstellt oder rekonstruiert werden:

```text
Erstelle eine eigenständige HTML/CSS/JavaScript-Website ohne Frameworks und mit möglichst wenigen Abhängigkeiten: einen Heizkosten- und Nebenkostenrechner für zwei Wohnungen EG und OG.

Kontext:
Zwei Wohnungen, EG und OG, teilen sich eine zentrale Gasheizung. Beide Wohnungen sind etwa 78 m² groß und sonst identisch. Die Heizung befindet sich im OG. Der Vermieter zahlt zunächst die Gasrechnung, EG zahlt zunächst Wasser/Abwasser und Allgemeinstrom. EG und OG leisten außerdem jährliche Gas-Vorauszahlungen an den Vermieter, die am Ende verrechnet werden.

Die Seite soll direkt als einzelne HTML-Datei im Browser funktionieren. Eingaben sollen optional per Button im LocalStorage gespeichert werden können. Es soll auch einen Button geben, der alle gespeicherten Werte aus dem LocalStorage löscht. Der Berechnen-Button soll optisch bündig zu den Eingabefeldern/Aktionsbuttons sein, gleiche Breite, gutes Padding, harmonisches Layout. Sections sollen leichte Hintergründe und abgerundete Ecken haben. Ergebnisdarstellung in übersichtlichen Tabellen mit Eurobeträgen und nachvollziehbaren Zwischenwerten.

Eingabefelder:
- Wohnfläche EG (m²), Standard 78
- Wohnfläche OG (m²), Standard 78
- Gaskosten gesamt (€), inklusive explizit ausgewiesener CO₂-Kosten
- Abrechnungszeitraum
- Abrechnungsdauer in Monaten, Standard 12
- CO₂-Kosten laut Gasrechnung (€)
- CO₂-Ausstoß laut Gasrechnung (kg)
- Gas-Vorauszahlung EG im Jahr (€)
- Gas-Vorauszahlung OG im Jahr (€)
- Wärmemengenzähler Heizkreis EG (kWh)
- Wärmemengenzähler Heizkreis OG (kWh)
- Wärmemengenzähler Warmwasser gesamt (kWh)
- Warmwasser EG (m³)
- Warmwasser OG (m³)
- Zwischenzähler Kaltwasser für Heizung/Warmwasser (m³)
- Frischwasserpreis (€/m³)
- Abwasserpreis (€/m³)
- Allgemeinstrom (Zählerstand gesamt, kWh)
- Heizungsstrom laut App (kWh)
- Strompreis (€/kWh)

Berechnung Gas:
Die eingegebenen Gaskosten enthalten bereits die CO₂-Kosten. Ziehe zuerst die explizit ausgewiesenen CO₂-Kosten ab. Nur die bereinigten Gaskosten werden anschließend auf Heizung und Warmwasser verteilt.

Aufteilung bereinigte Gaskosten:
- Kostenblock Heizung = bereinigte Gaskosten × Anteil Heizkreis-kWh an gesamter gelieferter Wärme
- Kostenblock Warmwasser = bereinigte Gaskosten × Anteil Warmwasser-kWh an gesamter gelieferter Wärme
- Gesamte gelieferte Wärme = Heizkreis EG + Heizkreis OG + Wärmemengenzähler Warmwasser gesamt

Für Heizung:
- 30 % Grundkosten nach Wohnfläche
- 70 % Verbrauchskosten nach Wärmemengenzähler Heizkreis EG/OG

Für Warmwasser:
- 30 % Grundkosten nach Wohnfläche
- 70 % Verbrauchskosten nach Warmwasserverbrauch in m³ EG/OG
- Der Warmwasser-Wärmemengenzähler bestimmt nur den Warmwasser-Kostenblock.

CO₂-Kosten:
Die CO₂-Kosten werden separat nach CO₂-Kostenaufteilungsgesetz verteilt. Dafür den spezifischen CO₂-Ausstoß berechnen:
CO₂ kg / Gesamtwohnfläche × 12 / Abrechnungsdauer in Monaten = kg CO₂/m²/a.

Nutze die gesetzliche Staffel:
- < 12 kg CO₂/m²/a: Mieter 100 %, Vermieter 0 %
- 12 bis < 17: Mieter 90 %, Vermieter 10 %
- 17 bis < 22: Mieter 80 %, Vermieter 20 %
- 22 bis < 27: Mieter 70 %, Vermieter 30 %
- 27 bis < 32: Mieter 60 %, Vermieter 40 %
- 32 bis < 37: Mieter 50 %, Vermieter 50 %
- 37 bis < 42: Mieter 40 %, Vermieter 60 %
- 42 bis < 47: Mieter 30 %, Vermieter 70 %
- 47 bis < 52: Mieter 20 %, Vermieter 80 %
- ≥ 52: Mieter 5 %, Vermieter 95 %

Den Vermieteranteil separat ausweisen. Den Mieteranteil verbrauchsabhängig auf EG und OG verteilen, proportional zur gelieferten Wärme je Wohnung:
- EG: Heizkreis EG + anteilige Warmwasserwärme nach Warmwasser-m³ EG
- OG: Heizkreis OG + anteilige Warmwasserwärme nach Warmwasser-m³ OG

Gas-Vorauszahlungen:
EG und OG haben im Jahr Gas an den Vermieter vorausgezahlt. Am Ende je Wohnung verrechnen:
Gas-Saldo = bereinigter Gasanteil + CO₂-Mieteranteil - Gas-Vorauszahlung.
Positive Werte sind Nachzahlung an Vermieter. Negative Werte sind Guthaben vom Vermieter. Beides in der Zusammenfassung getrennt ausweisen.

Wasser/Abwasser-Sonderfall:
Das Kaltwasser für die Heizung bzw. Warmwasserbereitung läuft über den Wasserzähler des EG. Es gibt einen separaten Zwischenzähler.
- Abwasser heißt in der Oberfläche einfach „Abwasser“.
- Abwasser entspricht der gesamten bezogenen Frischwassermenge laut Zwischenzähler.
- Der Teil der Frischwassermenge, der dem Warmwasserverbrauch entspricht, also Warmwasser EG + Warmwasser OG, wird verbrauchsabhängig nach m³ aufgeteilt.
- Die Differenz, z. B. Nachfüllung Heizkreis, wird 50/50 geteilt.
- Für Abwasser gilt dieselbe Mengenlogik, aber mit separatem Abwasserpreis.
- Ergebnis: Wasser/Abwasser wird zunächst vom EG bezahlt; OG muss seinen Anteil an EG erstatten.

Strom-Sonderfall:
Der Allgemeinstromzähler läuft über EG und beinhaltet auch den Heizungsstrom. In der Eingabe soll der gesamte Zählerstand eingetragen werden. Zusätzlich gibt es das Feld Heizungsstrom laut App.
Berechnung:
- Allgemeinstrom gesamt = gesamter Zählerstand × Strompreis
- Heizungsstrom = Heizungsstrom laut App × Strompreis
- Rest-Allgemeinstrom = Gesamtstrom - Heizungsstrom
- Rest-Allgemeinstrom wird 50/50 geteilt
- Heizungsstrom wird verbrauchsabhängig proportional zur gelieferten Wärme verteilt: Heizkreis + anteiliger Warmwasseranteil
In der Stromtabelle muss die Zeile exakt heißen:
„Allgemeinstrom (Zählerstand gesamt)“
Darunter eingerückt:
„davon Heizungsstrom (abgezogen)“
„davon Rest-Allgemeinstrom“

Ergebnistabellen:
Erstelle Tabellen für:
1. Gas ohne CO₂-Kosten: Aufteilung nach Wärmemenge und 30/70-Regel
2. CO₂-Kosten: Aufteilung nach CO₂-Kostenaufteilungsgesetz
3. Wasser: Kaltwasser für Warmwasser/Heizung über EG
4. Strom: Allgemeinstrom über EG, Heizungsstrom abgezogen
5. Zusammenfassung und Zahlungsflüsse

In den Tabellen neben Eurobeträgen immer auch Zwischenwerte zeigen, z. B. kWh, m³, Prozentanteile, 30/70-Beträge, CO₂-Stufe, Vermieteranteil, Mieteranteil, Vorauszahlungen, Nachzahlung/Guthaben.

Zusammenfassung:
Am Ende klar ausweisen:
- Kostenanteil EG gesamt
- Kostenanteil OG gesamt
- Vermieter trägt selbst: CO₂-Anteil Vermieter
- EG/OG Gas-Saldo gegenüber Vermieter nach Vorauszahlungen
- offene Nachzahlung an Vermieter
- Guthaben vom Vermieter
- OG erstattet an EG für Wasser/Abwasser und Strom
```
