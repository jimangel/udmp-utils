# udmp-utils

Inspired / borrowed from: https://github.com/Kashalls/udmp-utils

# Compiling Bird2

Ran on a x64 raspberry pi.

```
# ssh pi@[IP ADDRESS] 
curl https://get.docker.com/ | bash -

# add user to docker group
sudo usermod -a -G docker $USER

# run a debian container w/ python
sudo docker run --privileged --rm -it -v $PWD:/root/workdir arm64v8/python:3.6-slim-stretch bash

# update
apt update && apt install git dpkg-dev python3-pip -y && pip3 install apkg

# clone bird repo
git clone -b mh-bird-apkg https://gitlab.nic.cz/labs/bird.git && cd bird

# setup system
apkg system-setup

# get archive
apkg get-archive

# create source code
apkg srcpkg

# WE ARE HERE: build source code
apkg build --build-dep

# cp $OUTPUT.deb to /root/workdir/
cp pkg/pkgs/debian-9/bird2_2.0.8.1660433486.ebd5751c-cznic.1/bird2_2.0.8.1660433486.ebd5751c-cznic.1_arm64.deb  /root/workdir/

# drop out fo container
exit && exit

# scp the files and commit
cd ~/udmp-utils/bird/
scp jangel@IP ADDRESS]:/home/jangel/bird2_2.0.8.1660433486.ebd5751c-cznic.1_arm64.deb ./PATH/TO/DIR/bird2_2.0.8_arm64_jim.deb

# git add / commit / push
```

> details on apkg: https://pkg.labs.nic.cz/pages/apkg/guide/#apkg-packaging-workflow