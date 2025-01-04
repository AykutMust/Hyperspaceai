# Hyperspaceai
## We are running CLI on the server. First, let's go to the site and get the keys in the public key and private key sections shown in the image and save them somewhere. We will use them in the installation
Visit: https://node.hyper.space/

![Ekran Görüntüsü (1201)](https://github.com/user-attachments/assets/82d0e6aa-bf4c-4a40-92ed-fedb37e6b17d)

![Ekran Görüntüsü (1202)](https://github.com/user-attachments/assets/c8c0259f-0e98-4ee4-ab3b-8971573becf7)

### Install

```
curl https://download.hyper.space/api/install | bash

source ~/.bashrc
```

## Verify that the CLI is Working

```
aios-cli version
```

## Create Systemd Service File for CLI
```
sudo nano /etc/systemd/system/aios.service
```

## Add the following configuration into the file:
```
[Unit]
Description=aiOS CLI Service
After=network.target

[Service]
ExecStart=/root/.aios/aios-cli start
Restart=always
RestartSec=5
User=root
WorkingDirectory=/root
Environment=PATH=/usr/local/bin:/usr/bin:/bin:/root/.aios

[Install]
WantedBy=multi-user.target
```
# Save the service file and exit.(Ctrl x+y Enter)

## Let's make the adjustments

```
sudo cp /root/.aios/aios-cli /usr/local/bin/
```
```
sudo chmod +x /usr/local/bin/aios-cli
```

## Start and Activate the Service

```
sudo systemctl daemon-reload

sudo systemctl start aios.service

sudo systemctl enable aios.service

sudo systemctl status aios.service
```

#The output should be like this

![Ekran Görüntüsü (1204)](https://github.com/user-attachments/assets/1743b723-afd6-4372-a767-b1b0c5c4135e)

## Define the Wallet Key (We write the Private Key we got from the site. The quotation marks remain. The key in the 2nd photo I showed above.)

```
echo "PRİVATE KEY" > my-key.base58
```
```
aios-cli hive import-keys ./my-key.base58
```






