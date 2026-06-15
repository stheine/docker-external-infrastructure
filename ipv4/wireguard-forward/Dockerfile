FROM alpine:latest

# Set the shell environment
COPY docker_container_profile /root/.bash_profile

# Install
RUN \
  apk update && \
  apk --no-cache add \
    bash \
    socat \
    tzdata && \
  cp /usr/share/zoneinfo/Europe/Berlin /etc/localtime && \
  echo "Europe/Berlin" > /etc/timezone && \
  apk del tzdata

ENV TZ Europe/Berlin

CMD ["socat", "UDP4-LISTEN:50856,fork,su=nobody", "UDP6:wireguard6.heine7.de:50856"]


# sudo iptables -L INPUT --line-numbers -v
# sudo iptables -R INPUT 7 -p udp -m udp --dport 50856 -j ACCEPT
# sudo vi /etc/iptables/rules.v4
#   -A INPUT -p udp -m udp --dport 50856 -j ACCEPT
# docker compose build wireguard-forward
# docker compose up -d wireguard-forward
# netstat -tulpn | grep 'udp.*0 0\.0\.0\.0:'
