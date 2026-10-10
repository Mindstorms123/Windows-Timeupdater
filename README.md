### Installation & Einrichtung

Um die Zeitsynchronisation bei jedem Systemstart automatisch und komplett unsichtbar (ohne aufblinkendes Terminal-Fenster) auszuführen, nutze die Windows-Aufgabenplanung.

#### 1. Skript erstellen
Speichere den folgenden Code als `TimeSync.bat` an einem sicheren Ort (z. B. `C:\Skripte\TimeSync.bat`):

```batch
@echo off
net stop w32time
net start w32time
w32tm /resync
```

#### 2. Aufgabenplanung konfigurieren
1. Drücke `Win + R`, tippe `taskschd.msc` ein und drücke **Enter**, um die Aufgabenplanung zu öffnen.
2. Klicke auf der rechten Seite auf **Aufgabe erstellen...** (Achtung: Nicht "Einfache Aufgabe erstellen").
3. **Reiter "Allgemein":**
   * Vergib einen passenden Namen (z. B. `Windows Time Sync`).
   * Klicke auf **Benutzer oder Gruppe ändern...**, tippe das Wort `SYSTEM` in das Feld ein, klicke auf *Namen überprüfen* und bestätige mit **OK**. (Dies versteckt das Terminal-Fenster komplett).
   * Setze den Haken bei **Mit höchsten Privilegien ausführen** (erforderlich für den Zeitdienst).
4. **Reiter "Trigger":**
   * Klicke auf **Neu...**.
   * Wähle im oberen Dropdown-Menü **Beim Systemstart** (oder alternativ "Bei Anmeldung") und bestätige mit **OK**.
5. **Reiter "Aktionen":**
   * Klicke auf **Neu...**.
   * Belasse die Aktion auf **Programm starten**.
   * Klicke auf **Durchsuchen...**, wähle deine Datei `TimeSync.bat` aus und klicke auf **OK**.
6. **Reiter "Bedingungen" (Wichtig für Laptops):**
   * Entferne den Haken bei *Nur starten, wenn der Computer im Netzbetrieb ausgeführt wird*, damit das Skript auch im Akkubetrieb läuft.
7. Klicke abschließend auf **OK**, um die Aufgabe zu speichern. Das Skript läuft ab dem nächsten Neustart vollautomatisch und unsichtbar im Hintergrund.
