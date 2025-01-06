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

## Sign in:
```
aios-cli hive login
```
## Check session status:
```
aios-cli hive whoami
```
#The output will show the publickey and private key

## Tier Selection
```
aios-cli hive select-tier 5
```
## Download Required Model
```
aios-cli models add hf:TheBloke/phi-2-GGUF:phi-2.Q4_K_M.gguf
```

## Connect to Hive Network (wait until the command responds and moves to the directory. This is also valid for the following commands)
```
aios-cli hive connect
```
## Check your connection status and points

```
aios-cli hive points
```

# It should output like this

![Ekran Görüntüsü (1198)](https://github.com/user-attachments/assets/b9bbfac7-98d5-40c9-b3c6-d5fdd7e843bf)


# !!!!! If you get an error with model registration. download the model to ''cd /root/.aios'' directory... apply hive disconnect and connect commands.


## Monitor Logs
Check the logs to verify that the service is running properly and communicating with the Hive network:

```
sudo journalctl -u aios.service -f
```




## Resetting the Connection (If Problems Occur)
  # If you experience connection problems:
```
aios-cli hive disconnect
```
  # Try to connect again:
```
aios-cli hive connect
```



























