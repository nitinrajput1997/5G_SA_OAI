# 5G_SA_OAI

### Pre-requisite
```bash
sudo apt install -y git
sudo apt install net-tools
sudo apt install -y putty

sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"
sudo apt update
sudo apt install -y docker
sudo apt install -y docker-ce

# add your username to the docker group, otherwise you will have to run in sudo mode.
sudo usermod -a -G docker $(whoami)
reboot

# https://docs.docker.com/compose/install/
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Check pre-requistes
dpkg --list | grep docker
python3 --version

docker network create --driver=bridge --subnet=192.168.70.128/26 -o "com.docker.network.bridge.name"="demo-oai" demo-oai-public-net
sudo service docker restart
```
### Setup
```bash
git clone https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-fed.git ~/oai-cn5g-fed
cd ~/oai-cn5g-fed
git checkout master

cd ~/oai-cn5g-fed
./scripts/syncComponents.sh --nrf-branch develop --amf-branch develop --smf-branch develop --spgwu-tiny-branch develop --ausf-branch develop --udm-branch develop --udr-branch develop --upf-vpp-branch develop --nssf-branch develop

docker pull rdefosseoai/oai-amf:develop
docker pull rdefosseoai/oai-nrf:develop
docker pull rdefosseoai/oai-smf:develop
docker pull rdefosseoai/oai-udr:develop
docker pull rdefosseoai/oai-udm:develop
docker pull rdefosseoai/oai-ausf:develop
docker pull rdefosseoai/oai-upf-vpp:develop
docker pull rdefosseoai/oai-spgwu-tiny:develop
docker pull rdefosseoai/oai-nssf:develop

docker image tag rdefosseoai/oai-amf:develop oai-amf:develop
docker image tag rdefosseoai/oai-nrf:develop oai-nrf:develop
docker image tag rdefosseoai/oai-smf:develop oai-smf:develop
docker image tag rdefosseoai/oai-udr:develop oai-udr:develop
docker image tag rdefosseoai/oai-udm:develop oai-udm:develop
docker image tag rdefosseoai/oai-ausf:develop oai-ausf:develop
docker image tag rdefosseoai/oai-upf-vpp:develop oai-upf-vpp:develop
docker image tag rdefosseoai/oai-spgwu-tiny:develop oai-spgwu-tiny:develop
docker image tag rdefosseoai/oai-nssf:develop oai-nssf:develop
```
