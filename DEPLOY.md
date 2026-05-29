# Deploy na serwer — jednorazowe komendy

## 1. Skopiuj pliki na VPS

```bash
cd "/Users/michal/CLAUDE PROJECTS/PIN BALL"

ssh root@195.35.56.37 "mkdir -p /opt/pinball-demo"

scp game.html tlo_strony.png tlo_gry.png ball2.png pasek.png \
    k1.png k2.png k3.png k4.png k5.png k6.png \
    k7.png k8.png k9.png k10.png k11.png k12.png \
    root@195.35.56.37:/opt/pinball-demo/
```

## 2. Odpal nginx container na VPS

```bash
ssh root@195.35.56.37 "
  docker run -d --name pinball-demo \
    -p 8088:80 \
    -v /opt/pinball-demo:/usr/share/nginx/html:ro \
    nginx:alpine
"
```

## 3. Link do gry

http://195.35.56.37:8088/game.html

## Aktualizacja (gdy zmienisz pliki)

```bash
cd "/Users/michal/CLAUDE PROJECTS/PIN BALL"
scp game.html k*.png root@195.35.56.37:/opt/pinball-demo/
ssh root@195.35.56.37 "docker restart pinball-demo"
```

## Zatrzymanie / usunięcie

```bash
ssh root@195.35.56.37 "docker rm -f pinball-demo"
```
