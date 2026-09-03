# GroupAlarm Box Integration für Home Assistant

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)
![GitHub all releases](https://img.shields.io/github/downloads/groupalarm/box-ha/total)
## Hinweise

- Diese Integration **provisioniert** die GroupAlarm Box automatisch mit deinen Home-Assistant-MQTT-Einstellungen (Broker/Port/User/Pass/Prefix).
- Die Anzeige der Entitäten im Dashboard erfolgt **über MQTT Discovery** (Home Assistant MQTT Integration).  
  Ohne MQTT Discovery siehst du in Home Assistant **keine automatisch erzeugten** Entitäten.

## Beschreibung

Die `groupalarmbox` Integration findet deine GroupAlarm Box im Netzwerk automatisch und sendet anschließend die MQTT-Konfiguration an die Box.

Die Box veröffentlicht danach:
- den Status (`alive`) und
- Alarme (`alarm`)

…und legt via MQTT Discovery zwei `binary_sensor`-Entitäten an (z. B. *Alive* und *Alarm*).

## Voraussetzungen

1. **MQTT in Home Assistant** muss eingerichtet sein:
   
2. In der Home Assistant MQTT Integration muss **Discovery** aktiv sein (Standard: `homeassistant` als Discovery Prefix).

> Wichtig: Der “Discovery Prefix” in Home Assistant muss zu dem passen, was die Box für Discovery nutzt  
> (typisch: `homeassistant`). Wenn du hier z. B. `groupalarmbox` verwendest, muss Home Assistant ebenfalls diesen Prefix nutzen.

## Installation
  [![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=groupalarm&repository=box-ha&category=Integration)
### Option A: HACS (empfohlen)

1. HACS öffnen
2. **Integrationen** → **Benutzerdefinierte Repositories** hinzufügen
3. Repository URL eintragen und als **Integration** hinzufügen
4. Integration installieren
5. Home Assistant neu starten

### Option B: Manuell

1. Öffne dein Home Assistant Konfigurationsverzeichnis.
2. Falls noch nicht vorhanden, erstelle `custom_components/`.
3. Erstelle den Ordner `custom_components/groupalarmbox/`.
4. Kopiere alle Dateien aus diesem Repository nach `custom_components/groupalarmbox/`.
5. Starte Home Assistant neu.
6. Integration hinzufügen (siehe **Konfiguration**).

## Konfiguration

Die Konfiguration erfolgt komplett über die Home Assistant UI.

**Einstellungen ➤ Geräte & Dienste ➤ Integrationen ➤ ➕ Integration hinzufügen ➤ „GroupAlarm Box“**


### Was trage ich bei „Target“ ein?

- **Wenn Zeroconf funktioniert:** meist nichts – die Box wird automatisch erkannt.
> Tipp: Wenn du im Log siehst „Provisioned … via UDP“, dann hat das Provisioning funktioniert.

## MQTT Topics (Überblick)

Nach erfolgreichem Provisioning nutzt die Box typischerweise Topics nach diesem Muster:

- Status/Availability:  
  `groupalarmbox/<mac>/status`
- Alive:  
  `groupalarmbox/<mac>/alive`
- Alarm:  
  `groupalarmbox/<mac>/alarm`

MQTT Discovery Config Topics (Beispiel):
- `homeassistant/binary_sensor/<mac>/alive/config`
- `homeassistant/binary_sensor/<mac>/alarm/config`


## Troubleshooting

### 1) „Provisioning klappt, aber keine Entitäten erscheinen“
Prüfe:

1. **MQTT Integration in Home Assistant aktiv?**  
   Einstellungen → Geräte & Dienste → MQTT muss „konfiguriert“ sein.
2. **Discovery Prefix passt?**  
   MQTT → Konfigurieren → „Discovery Prefix“ (Standard: `homeassistant`)
3. **Kommen Discovery Messages an?**  
   Entwicklerwerkzeuge → MQTT → „Auf ein Topic lauschen“  
   - lausche auf `homeassistant/#` (oder deinen Prefix)  
   - du solltest `.../config` Nachrichten sehen.

### 2) „Home Assistant erkennt die Box nicht“
- Stelle sicher, dass mDNS/Multicast im Netzwerk nicht geblockt wird.
- 
## Lizenz

Dieses Projekt ist **source-available**, aber **nicht Open Source**.

Siehe: [`LICENSE`](LICENSE)
(CUBOS INTERNET GMBH PUBLIC USE LICENSE – No Derivatives, No Redistribution)

---

[commits-shield]: https://img.shields.io/github/commit-activity/y/groupalarm/box-ha?style=for-the-badge
[commits]: https://github.com/groupalarm/box-ha/commits/main
[hacs]: https://github.com/custom-components/hacs
[hacsbadge]: https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge
[license-shield]: https://img.shields.io/github/license/groupalarm/box-ha?style=for-the-badge
