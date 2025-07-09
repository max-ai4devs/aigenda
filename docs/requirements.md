# Anforderungen AIgenda

## 1. Einführung  
- _AIgenda ist eine Web-App für Trainer, um zu Beginn einer Schulung flexibel und effizient die Tagesagenda zu planen und automatisiert abzuspielen._  
- _Ziel: KI-gestützte Slotplanung basierend auf natürlicher Spracheingabe und synchrone Countdown-Visualisierung für Trainer und Teilnehmer._

---

## 2. User Stories  
> _ID, Titel, Story und Akzeptanzkriterien_

- **US-01: Agenda aus Sprache erzeugen**  
  - **Story:** Als Trainer möchte ich Beginn, Ende und Mittagspause einer Schulung in natürlicher Sprache eingeben, damit AIgenda mir automatisch eine plausible Tagesagenda mit Pausen und Schulungsslots vorschlägt.  
  - **Akzeptanzkriterien:**  
    - Text-Eingabe wie „Beginn 09:00, Ende 17:00, Mittagspause 12:30 für 45 Minuten“ erzeugt zwei alternative Agenden  
    - Jede Agenda enthält gleichmäßige Slots von 35-60 Minuten und Pausen von 5 oder 10 Minuten  
    - Vorschläge werden in Markdown-Tabellen ausgegeben  
    - Jede Agenda ist mit einem Satz kommentiert (z.B. „gleichmäßige Verteilung“)

- **US-02: Countdown starten und abspielen**  
  - **Story:** Als Trainer möchte ich die gewählte Agenda per Klick starten, damit die Schulung automatisiert abläuft und ich akustisch sowie visuell an Slotwechsel erinnert werde.  
  - **Akzeptanzkriterien:**  
    - „Play“-Button startet die gewählte Agenda  
    - Countdown pro Slot läuft automatisch, beginnt sofort beim nächsten Slot  
    - Doorbell-Sound erklingt beim Slotwechsel  
    - Aktueller Slot und verbleibende Zeit sind immer sichtbar  
    - Im Browser-Tab wird verbleibende Zeit angezeigt:
      - Alle 3 Minuten aktualisiert
      - Unter 3 Minuten orange, unter 1 Minute rot und fett
      - Unter 20 Sekunden sekundengenau

- **US-03: Teilnehmeransicht teilen**  
  - **Story:** Als Trainer möchte ich einen QR-Code erzeugen können, damit Teilnehmer die laufende Agenda in ihrem Browser mitverfolgen und akustische Signale ebenfalls wahrnehmen können.  
  - **Akzeptanzkriterien:**  
    - QR-Code wird generiert und zeigt eine „Read-Only“-Ansicht der Agenda  
    - Countdown und Doorbell-Ton werden synchron mit der Trainer-Ansicht abgespielt  
    - Teilnehmer können nichts verändern  
    - Zugriff nur während laufender Session gültig

---

## 3. Non‑functional Requirements  

- **Performance:**  
  - Anzeige der Countdown-Ansicht erfolgt innerhalb von 300ms  
  - Serverantwortzeit auf Chat-Eingaben < 1 Sekunde  

- **Security:**  
  - Trainer-Authentifizierung erfolgt über mitgesendetes Token im HTTP-Header  
  - Teilnehmer-Zugriff nur über QR-Code-Link ohne Schreibrechte  
  - HTTPS-Verbindung ist obligatorisch  

- **Robustheit:**  
  - Countdown berücksichtigt tatsächliche Systemzeit  
  - Bei verspätetem Start wird verstrichene Zeit abgezogen  
  - Bei frühem Start: Countdown bis Agenda-Beginn sichtbar  

---

## 4. Release‑Plan  
| Story‑ID | Kurzbeschreibung                  | Priorität | Geplantes Release |
|----------|-----------------------------------|-----------|-------------------|
| US-01    | Agenda aus Sprache erzeugen       | **MVP**   | Version 1.0.0     |
| US-02    | Countdown starten und abspielen   | **MVP**   | Version 1.0.0     |
| US-03    | Teilnehmeransicht teilen          | **MVP**   | Version 1.0.0     |
