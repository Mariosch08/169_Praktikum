# VPN + Monitoring – M169 Praktikum


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


```

**### 1. Stack starten**

```bash
docker compose up -d
```

### 2. Stack stoppen

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
1860 ist als standard definiert


## Client-Konfiguration (WireGuard)

Nach dem ersten Start generiert der WireGuard-Container automatisch Client-Configs:

```bash
# QR-Code für Client anzeigen (z.B. Peer 1)
docker exec wireguard /app/show-peer 1

# Config-Datei direkt anzeigen
cat ./wireguard/config/peer1/peer1.conf
```
