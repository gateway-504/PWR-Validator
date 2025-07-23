# PWR Validator Node Guide

Important Note: This is the inaugural testnet launch. While we strive for perfection, there might be unforeseen issues. We appreciate all feedback, bug reports, or any other issues reported in our Discord server.

## Requirements: 
- **CPU**: 2 vCPU
- **Memory**: 4 GB RAM  
- **Disk**: 100 GB HDD or higher
- **Bandwidth**: 900Mbps or higher
- **Open TCP Ports**: 8231, 8085, 9864
- **Open UDP Ports**: 7621

## Setup on Ubuntu Server


### 1.update OS


```
sudo apt update 
```


### 2. Install Java

#### Download OpenJDK 21.0.7 (Temurin JDK)


```
wget https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.7%2B6/OpenJDK21U-jdk_x64_linux_hotspot_21.0.7_6.tar.gz
```

#### Extract and Move


```
tar -xzf OpenJDK21U-jdk_x64_linux_hotspot_21.0.7_6.tar.gz
mv jdk-21.0.7+6 /usr/local/java-21
```

####Set Environment Variables

```
export JAVA_HOME=/usr/local/java-21
export PATH=$JAVA_HOME/bin:$PATH
echo 'export JAVA_HOME=/usr/local/java-21' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```


#### Verify Installation

```
java -version
```

#### Expected output:
```
openjdk 21.0.7 2025-04-15 LTS
OpenJDK Runtime Environment Temurin-21.0.7+6 (build 21.0.7+6-LTS)
OpenJDK 64-Bit Server VM Temurin-21.0.7+6 (build 21.0.7+6-LTS, mixed mode, sharing)
```

##### Verify JDK:

```
javac -version
```

#### Expected output:
```
javac 21.0.7.
```

### 3. Open Required Ports

For UFW (Uncomplicated Firewall):

```
sudo ufw allow 8231/tcp
sudo ufw allow 8085/tcp
sudo ufw allow 9864/tcp
sudo ufw allow 7621/udp
sudo ufw reload
```


### 4. Install the validator node software and config file

```
wget https://github.com/pwrlabs/PWR-Validator/releases/download/15.58.2/validator.jar
wget https://github.com/pwrlabs/PWR-Validator/raw/refs/heads/main/config.json
```



### 5. Setup your password

```
echo "your password here" > password
```

### 6.create new tmux session 

```
apt install tmux

tmux new -s pwr
```

### 7. Run the Node
Replace <YOUR_SERVER_IP> with your server's actual IP.

```
java --enable-native-access=ALL-UNNAMED -Xms1g -Xmx6g -jar validator.jar --ip <your nodes ip here> --password password &
```


detach session with ctrl b+d

**Note:** Make sure ports 8085 and 8231 are open for TCP.

### 8. Get Your Address

```
java -jar validator.jar get-address password
```


### 9. Become a Validator Node
Initially, your node will synchronize with the blockchain but will not assume validator responsibilities until it possesses staked PWR Coins.
To obtain sufficient PWR Coins for staking, [apply to become a testnet validator](https://docs.google.com/forms/d/1ImUgk8JaKCwJR-7xiBNaA8-mb604CYdSKJfMRHacA60) . Once approved, you can use PWR discord bot to claim 100k PWR to stake.

After claiming your coins, your node will initiate a transaction to enlist as a validator.

### 10. Checking your nodes log
If you wish to check your nodes log, you can do so using the following command:


```
tmux attach -t pwr
```


#### Congratulations, you've now set up and run a PWR Chain validator node!



#### Importing an Existing Wallet
To import your old wallet using this update:

```
java -jar validator.jar import-seed-phrase <password file here> <seed phrase here>
```
Example:

```
java -jar validator.jar import-seed-phrase password public neither spider scare diagram knife fragile road kit guess crucial bachelor
```
