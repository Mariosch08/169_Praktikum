# Prometheus Monitoring – eigenes Image
# Basis: offizielles Prometheus Image
FROM prom/prometheus:latest

LABEL maintainer="YOUR_TEAM_NAME"
LABEL description="Prometheus Monitoring fuer WireGuard VPN – M169 Praktikum"
LABEL version="1.0"

# Eigene Konfiguration ins Image kopieren
COPY prometheus.yml /etc/prometheus/prometheus.yml

# Port fuer Prometheus Web UI und API
EXPOSE 9090

# Prometheus mit unserer Konfiguration starten
CMD ["--config.file=/etc/prometheus/prometheus.yml", \
     "--storage.tsdb.path=/prometheus", \
     "--web.console.libraries=/usr/share/prometheus/console_libraries", \
     "--web.console.templates=/usr/share/prometheus/consoles", \
     "--web.enable-lifecycle"]
