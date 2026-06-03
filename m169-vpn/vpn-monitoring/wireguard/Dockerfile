# WireGuard VPN – eigenes Image
# Basis: linuxserver/wireguard (Debian-basiert, ARM + x86 kompatibel)
FROM lscr.io/linuxserver/wireguard:latest

# Metadaten
LABEL maintainer="M169_praktikum"
LABEL description="WireGuard VPN Server fuer das M169 Praktikum"
LABEL version="1.0"

# Standard-Umgebungsvariablen (koennen per docker-compose ueberschrieben werden)
ENV PUID=1000 \
    PGID=1000 \
    TZ=Europe/Zurich \
    SERVERPORT=51820 \
    PEERS=3 \
    INTERNAL_SUBNET=10.13.13.0 \
    PEERDNS=auto \
    LOG_CONFS=true

# Port fuer WireGuard UDP
EXPOSE 51820/udp

# Healthcheck: prueft ob das wg0-Interface aktiv ist
HEALTHCHECK --interval=30s --timeout=10s --start-period=15s --retries=3 \
    CMD wg show wg0 || exit 1
