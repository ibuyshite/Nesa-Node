## Requirements


- You must need to buy a VPS for running Nesa Node
- Buy VPS which is fulfilling all these requirements : 
```bash
Operating System : Ubuntu 22.04
CPU : Minimum of 4 core
RAM : 4GB Minimum
Storage : SSD or NVMe with at least 50GB of space
```

## Create Wallet & Request Faucet

- Install : [Leap Extension](https://chromewebstore.google.com/detail/leap-cosmos-wallet/fcfcfllfndlomdhbehjjcoimbgofdncg)
- Create a New Wallet / Import From KEplr
- Export Private Keys Because We Gonna Need Later

## Install dependecies
```console
# Install Packages
sudo apt update & sudo apt upgrade -y

sudo apt install ca-certificates zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev curl git wget make jq build-essential pkg-config lsb-release libssl-dev libreadline-dev libffi-dev gcc screen unzip lz4 -y
```

```console
# Install Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version

# Install Docker-Compose
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version

# Docker Permission to user
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Obtain a Hugging Face API key
1. Visit the [Hugging Face website](https://huggingface.co/).

2. Sign up or log in to your account.

3. Navigate to your [API access tokens page](https://huggingface.co/settings/tokens) under your account settings.

4. Click **“Create new token”**, head to **“Write”** tab, and generate an API key by clicking on **“Create token”** .

5. Copy the generated key to use it in your miner installation.

##  Step 4: Open Ports
```console
sudo ufw allow ssh
sudo ufw allow 22
sudo ufw allow 31333
sudo ufw enable
```

## Install and run Nesa Miner
```
bash <(curl -s https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh)
```
* **Select a mode**: Choose **Wizardy**.
* **Choose a Moniker**: Provide a unique name for your node.
* **Node hostname**: skip & press `Enter`.
* **Node email**: skip & press `Enter`.
* **Enter Referral Code: to get bonus points**: `nesa1ca0dt3rsdu20003pruj8hsk7qs6fgd0aqfmmtc`
* **Wallet Private Key**: Enter your wallet private key for miner registration and to receive rewards.
* Finalize Configuration: Review and confirm the configuration before starting your node. The bootstrap script will provide a summary of your configuration and allow you to make changes before starting the miner.

![image](https://github.com/user-attachments/assets/69540b5a-1461-41a4-8a20-6efe4d5686f7)

##  Step 6: Useful commands

### Check container logs
```
docker logs -f orchestrator
```
```
docker logs -f mongodb
```

Check Containers: You must have 4 new containers now
```
docker ps
```

### Get node peer-id (wallet public key)
```console
cat $HOME/.nesa/identity/node_id.id
```

### Get node status url
```
PUB_KEY=$(cat $HOME/.nesa/identity/node_id.id)
echo https://node.nesa.ai/nodes/$PUB_KEY
```
![image](https://github.com/user-attachments/assets/1c33ea05-6d59-4c7e-a061-76324b2e0134)

## OptionaL: Update or Restart node
* For existing nodes that just need to update their configuration or restart their node

```
bash <(curl -s https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh)
```

**1. select "Advanced Wizardry"**

**2. Select Yes to bootstrap it, even if it is currently running.**

* This will update your config and reboot the containers if they are running or start them if they are not.

* After this, use `cat ~/.nesa/identity/node_id.id` to check your **node_id** and make sure it is as you think it is. Check the stats at https://node.nesa.ai/

## Tokenomic:
The $NES token will be launched on the mainnet network, and 8.8% of it will be airdropped to the incentivized testnet participants.

![GMpSQF5XAAABwMI](https://github.com/user-attachments/assets/a3bb334d-a55a-41f8-9a04-a333444e04fe)
