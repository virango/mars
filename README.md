# Mars Energy Controller - Docker Setup

## Feature
- Python-Skript für Batterie- und Smartmeter-Steuerung via MQTT
- Vollständig containerisiert in Docker
- Konfigurierbar über Umgebungsvariablen
- Logs werden direkt zu Docker-Output gestreamt

## Voraussetzungen
- Docker und Docker Compose installiert
- Zugang zu MQTT Broker (Standard: 192.168.178.6:1883)
- Zugang zu Smart Meter (Standard: 192.168.178.53:12345)

## Setup

### 1. Image bauen
```bash
docker-compose build
```

### 2. Container starten
```bash
docker-compose up -d
```

### 3. Logs anschauen
```bash
docker-compose logs -f mars
```

### 4. Container stoppen
```bash
docker-compose down
```

## Konfiguration

Bearbeite `docker-compose.yml` um die IP-Adressen und Ports anzupassen:

```yaml
environment:
  - MQTT_BROKER_IP=192.168.178.6
  - MQTT_BROKER_PORT=1883
  - SMARTMETER_IP=192.168.178.53
  - SMARTMETER_PORT=12345
```

Oder kopiere `.env.example` zu `.env` und lade die Werte von dort:
```bash
cp .env.example .env
# Bearbeite .env mit deinen Werten
docker-compose up -d
```

## Debugging
```bash
# Live-Logs mit Zeitstempel
docker-compose logs -f --timestamps mars

# Nur letzte 100 Zeilen
docker-compose logs --tail=100 mars

# Container Info
docker ps
docker inspect mars-energy-controller
```

## Restart-Policy
Der Container startet automatisch neu bei Fehler oder Host-Reboot.
Deaktiviere das mit: `restart: "no"` in `docker-compose.yml`
