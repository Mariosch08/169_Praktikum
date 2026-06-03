# VPN + Monitoring – M169 Praktikum

WireGuard VPN mit Prometheus/Grafana Monitoring, betrieben via Docker Compose auf DietPi (Debian).

---

## Projektstruktur

```
vpn-monitoring/
├── docker-compose.yml          ← Orchestrierung aller Services
├── wireguard/
│   └── Dockerfile              ← Eigenes WireGuard Image
├── prometheus/
│   ├── Dockerfile              ← Eigenes Prometheus Image
│   └── prometheus.yml          ← Scrape-Konfiguration
└── grafana/
    ├── Dockerfile              ← Eigenes Grafana Image
    └── provisioning/
        ├── datasources/
        │   └── prometheus.yml  ← Prometheus automatisch einbinden
        └── dashboards/
            └── dashboard.yml   ← Dashboard-Quelle definieren
```

---

## Services

| Service | Port | Beschreibung |
|---|---|---|
| WireGuard | 51820/UDP | VPN Server |
| Node Exporter | 9100 | Systemmetriken (Durchsatz, CPU, RAM) |
| Prometheus | 9090 | Metriken sammeln und speichern |
| Grafana | 3000 | Dashboard (admin / admin123) |

---

## Setup

### 1. Docker Hub Benutzername setzen

In `docker-compose.yml` alle `YOUR_DOCKERHUB_USERNAME` ersetzen:

```bash
sed -i 's/YOUR_DOCKERHUB_USERNAME/euer_username/g' docker-compose.yml
```

### 2. Images bauen

```bash
docker compose build
```

### 3. Images auf Docker Hub pushen

```bash
docker login

docker push euer_username/wireguard:latest
docker push euer_username/prometheus:latest
docker push euer_username/grafana:latest
```

### 4. Stack starten

```bash
docker compose up -d
```

### 5. Stack stoppen

```bash
docker compose down
```

---

## Monitoring

### Grafana Dashboard

Grafana im Browser öffnen: `http://<DietPi-IP>:3000`  
Login: `admin` / `admin123`

Empfohlenes Dashboard importieren: **Node Exporter Full** (ID: `1860`)  
→ Dashboards → Import → ID eingeben → Load

### VPN-Durchsatz messen (PromQL)

Eingehender Durchsatz auf dem wg0-Interface:
```
rate(node_network_receive_bytes_total{device="wg0"}[5m]) * 8
```

Ausgehender Durchsatz:
```
rate(node_network_transmit_bytes_total{device="wg0"}[5m]) * 8
```

### Uptime prüfen

```
up{job="node-exporter"}
```

---

## Client-Konfiguration (WireGuard)

Nach dem ersten Start generiert der WireGuard-Container automatisch Client-Configs:

```bash
# QR-Code für Client anzeigen (z.B. Peer 1)
docker exec wireguard /app/show-peer 1

# Config-Datei direkt anzeigen
cat ./wireguard/config/peer1/peer1.conf
```

---

## Durchsatz-Test mit iperf3

```bash
# Auf dem Server (ausserhalb des Tunnels)
iperf3 -s

# Auf dem Client (durch den VPN-Tunnel)
iperf3 -c <VPN-Server-IP>
```
