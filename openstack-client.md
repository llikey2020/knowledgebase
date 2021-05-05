# Openstack Client

To install the openstack CLI:

```shell
sudo apt install -y python3 python3-pip
python3 -m pip install -U pip
python3 -m pip install python-openstackclient python-magnumclient
```

Download your Openstack RC file from the web GUI (top left menu).
Before running the client, source the RC file - it contains all of the values needed to connect as your user.

```shell
source myrc.sh
openstack versions show
```
