# [steps to reproduce:](https://reangdblog.blogspot.com/2016/05/chrome-docker.html)
Dockerfile
```Dockerfile
FROM 127.0.0.1:1027/arpa/ip6/c/f/ubuntu

ADD https://dl.google.com/linux/linux_signing_key.pub /tmp/
COPY run_chrome /bin/
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
  apt-get install -y --no-install-recommends dbus-x11 libexif12 && \
    chmod +x /bin/run_chrome && \
  apt-key add /tmp/linux_signing_key.pub && \
  echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable && \
  apt-get clean -y && \
    groupadd --gid 9999 docker && \
    useradd --password='' --uid=9999 --gid=docker --shell=/bin/bash --create-home docker

CMD /bin/run_chrome
```
run_chrome
```bash
#!/bin/bash

EXISTS=$(getent group hostgroup)
if [ "$EXISTS" == "" ]; then
groupadd -g $HOST_GID -o hostgroup
usermod -u $HOST_UID -g $HOST_GID docker
chown docker:hostgroup \
    /home/docker/.config/ \
    /home/docker/.config/google-chrome \
    /home/docker/.cache \
    /home/docker/.cache/google-chrome \
    /home/docker/Downloads
fi

su - docker -c google-chrome
```
chrome.sh
```sh
#!/bin/bash

STATE=$(docker ps --all --filter="name=chrome" --format="exists")
if [ "$STATE" == "" ]
then
docker run -d \
  --name=chrome \
  --cap-add=SYS_ADMIN \ 
```
```sh
  --security-opt seccomp:unconfined \
```
```sh
  --net=host \
  --env="DISPLAY" \
  --env="HOST_UID=$(id -u)" \
  --env="HOST_GID=$(id -g)" \
  --device /dev/snd \
  --log-driver=journald \
  --volume="/etc/localtime:/etc/localtime:ro" \
  --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
  --volume="/dev/shm:/dev/shm:rw" \
  --volume="$HOME/downloads:/home/docker/Downloads:rw" \
  --volume="/usr/share/icons:/usr/share/icons:ro" \
  --volume="/usr/share/fonts:/usr/share/fonts:ro" \
  --volume="/etc/fonts:/etc/fonts:ro" \
  --volume="/var/run/dbus/system_bus_socket:/var/run/dbus/system_bus_socket:ro" \
  --volume="$HOME/.Xauthority:/home/docker/.Xauthority:ro" \
  --volume="$HOME/.cache/google-chrome-cache:/home/docker/.cache/google-chrome:rw" \
  --volume="$HOME/.cache/google-chrome-config:/home/docker/.config/google-chrome:rw" \
  chrome
else
  docker start chrome
fi
```
docker build -t chrome .

Failed 
busted