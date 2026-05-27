# Grafana Dashboard – eigenes Image
# Basis: offizielles Grafana Image
FROM grafana/grafana:latest

LABEL maintainer="M169_praktikum"
LABEL description="Grafana Monitoring Dashboard fuer WireGuard VPN – M169 Praktikum"
LABEL version="1.0"

# Grafana laeuft als root im Container (fuer Provisioning noetig)
# Provisioning-Konfigurationen ins Image kopieren
# 472 = Grafana UID im offiziellen Image
COPY --chown=472:472 provisioning/ /etc/grafana/provisioning/

# Port fuer Grafana Web UI
EXPOSE 3000
