# Grafana Dashboard – eigenes Image
# Basis: offizielles Grafana Image
FROM grafana/grafana:latest

LABEL maintainer="YOUR_TEAM_NAME"
LABEL description="Grafana Monitoring Dashboard fuer WireGuard VPN – M169 Praktikum"
LABEL version="1.0"

# Grafana laeuft als root im Container (fuer Provisioning noetig)
USER root

# Provisioning-Konfigurationen ins Image kopieren
# → Prometheus-Datasource wird automatisch eingerichtet beim Start
COPY provisioning/ /etc/grafana/provisioning/

# Berechtigungen setzen
RUN chown -R grafana:grafana /etc/grafana/provisioning/

USER grafana

# Port fuer Grafana Web UI
EXPOSE 3000
