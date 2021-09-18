# Idena Service

In this repository you will find tool to run Idena as a systemd service.

I work with /home/centos/idena/ for Idena directory.


## 1 - Create service

Create the idena.service file and copy&paste the content of idena.service file from this repo or upload it with scp.

### 1.1 - Manual creation

Create a idena.service file
```shell
sudo touch /etc/systemd/system/idena.service
```

For edit it
```shell
sudo vim /etc/systemd/system/idena.service
```
And copy&paste the content

### 1.2 - Uploal creation

```shell
$ scp idena.service username@to_host:/etc/systemd/system/idena.service
```

### 1.3 - Start service

First we need to change permision

```shell
sudo chmod 644 /etc/systemd/system/idena.service
```

and we run it

```shell
sudo systemctl enable idena
```

## 2 - Update Idena with new release

On new idena release we need to stop service, update and restart

```shell
sudo systemctl stop idena

cd /home/centos/idena/

mv idena-go oldversion/

curl -s https://api.github.com/repos/idena-network/idena-go/releases/latest | grep browser_download_url | grep idena-node-linux-0.* | cut -d '"' -f 4 | wget -qi -

mv idena-node-linux* idena-go

sudo chmod +x idena-go

sudo systemctl daemon-reload

sudo systemctl start idena
```


Enjoy