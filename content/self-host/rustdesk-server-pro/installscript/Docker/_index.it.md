---
title: Docker
weight: 3
---

## Docker Compose (Raccomandato)

Con Docker Compose DEVI usare `network_mode: "host"` per garantire che le licenze funzionino. Installa Docker usando questa [guida](https://docs.docker.com/engine/install) per assicurarti che sia aggiornato!

Copia quanto segue in `compose.yml`.

```yaml
services:
  hbbs:
    container_name: hbbs
    image: docker.io/rustdesk/rustdesk-server-pro:latest
    command: hbbs
    volumes:
      - ./data:/root
    network_mode: "host"

    depends_on:
      - hbbr
    restart: unless-stopped

  hbbr:
    container_name: hbbr
    image: docker.io/rustdesk/rustdesk-server-pro:latest
    command: hbbr
    volumes:
      - ./data:/root
    network_mode: "host"
    restart: unless-stopped
```

Quindi esegui `sudo docker compose up -d` o `podman-compose up -d`

> `sudo apt install podman-compose` per l'installazione di `podman-compose`

{{% notice note %}}
Come [configurare HTTPS per la console web manualmente](https://rustdesk.com/docs/en/self-host/rustdesk-server-pro/faq/#set-up-https-for-web-console-manually).
{{% /notice %}}

## Comandi Docker

Installa Docker con questa [guida](https://docs.docker.com/engine/install) per assicurarti che sia aggiornato!

Oppure puoi installare docker con questo singolo comando.

```
bash <(wget -qO- https://get.docker.com)
```

Esegui i seguenti comandi (l'immagine s6 potrebbe necessitare di `./data:/data` invece di `./data:/root`):

```sh
sudo docker image pull rustdesk/rustdesk-server-pro
sudo docker run --name hbbs -v ./data:/root -td --net=host --restart unless-stopped docker.io/rustdesk/rustdesk-server-pro hbbs
sudo docker run --name hbbr -v ./data:/root -td --net=host --restart unless-stopped docker.io/rustdesk/rustdesk-server-pro hbbr
```

{{% notice note %}}
L'esempio sopra usa `sudo` e `--net=host`, questo non funzionerà su Windows, rimuovi questi comandi, se rimuovi `--net=host` controlla sotto.
{{% /notice %}}

```sh
macaddrhbbs=$(echo -n A0-62-2F; dd bs=1 count=3 if=/dev/random 2>/dev/null |hexdump -v -e '/1 "-%02X"')
sudo docker run --name hbbs -p 21114:21114 -p 21115:21115 -p 21116:21116 -p 21116:21116/udp -p 21118:21118 -v ./data:/root -td --mac-address="$macaddrhbbs" --restart unless-stopped docker.io/rustdesk/rustdesk-server-pro hbbs
sudo docker run --name hbbr -p 21117:21117 -p 21119:21119 -v ./data:/root -td --restart unless-stopped docker.io/rustdesk/rustdesk-server-pro hbbr
```

{{% notice note %}}
Come [configurare HTTPS per la console web manualmente](https://rustdesk.com/docs/en/self-host/rustdesk-server-pro/faq/#set-up-https-for-web-console-manually).
{{% /notice %}}


> Se hai problemi con SELinux su Fedora, controlla questo [problema](https://github.com/rustdesk/rustdesk-server/issues/230).