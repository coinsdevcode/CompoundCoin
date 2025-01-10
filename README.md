
# CompoundCoin


http://compoundcoin.org/            Official Website <br>
https://chainz.cryptoid.info/comp/  ( Blockexplorer including API )<br>
https://comp.ccore.online/          ( Blockexplorer including API )<br>
https://comp.coinexplorers.org/     
<br>
Hashing algorithm: x11<br>
Proof type: Proof-of-Stake<br>
Block time:120 seconds (2 minutes)<br>
Coin maturity:24 hours<br>
Staking period:minimum 24 hours<br>
Staking rewards:<br>
Up to block 1999999. 31.25% per year<br>
From block 2000000 to block 2499999. 15.625% per year<br>
After block 2500000. 7.8125% per year<br>
Transaction fee:min 0,25 coin<br>
Coinbase maturity:40 confirmations<br>
Supply:unlimited<br>


## How to compile and use the Linux Deamon
Tested and working on Ubtunu 14 - 16.04 and 18.04 Version.
Versions 20.04 and later do not currently compile due to changes in OpenSSL 1.1
and the Boost C++ library in that version.

### Swapfile

You can check if your server has a swap file already with the ```swapon``` command.  If your system has less than 1.5GB of memory, you'll want at least a 2GB swap area.  Add a new swapfile with:
```
sudo fallocate -l 2G /swapfile
sudo chown root:root /swapfile
sudo chmod 0600 /swapfile
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"
sudo mkswap /swapfile
sudo swapon /swapfile
```
If fallocate doesn’t work, you can instead use:
```
sudo dd if=/dev/zero of=/swapfile bs=1024 count=1024288
```
Initialize the swapfile to mount automatically on boot:
```
sudo echo '/swapfile none swap sw 0 0' >> /etc/fstab
```

### Install all required dependencies

```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get -y install nano ntp unzip git build-essential libssl-dev
sudo apt-get -y installlibdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude
sudo aptitude -y install miniupnpc libminiupnpc-dev
```
ubuntu 18.04
```
sudo apt-get install libssl1.0-dev
sudo apt-get install libqt4-dev
```

If you get an error mentioning lock files, you probably have a desktop or background package update tool running that prevents other apt changes from happening.  You can use the ```lsof``` utility to figure out what program holds the lock and then pause it from running.

Pull the source code from github, or download it yourself:
```
git clone https://github.com/coinsdevcode/CompoundCoin.git
```

### Compiling the software

Now you compile the included leveldb:
```
chmod +x CompoundCoin
cd CompoundCoin/src/leveldb
chmod +x build_detect_platform
make clean
make libleveldb.a libmemenv.a
```
Return to the source directory, and compile the daemon:
```
cd ..
make -f makefile.unix RELEASE=1
```
To compile qt (wallet with GUI) for Ubuntu 16.04 or 18.04 LTS use:
```
sudo apt-get install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools
sudo apt-get install libboost-system-dev
sudo apt-get install libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev
```
Return to the source directory, and compile the qt:
```
cd ..
qmake RELEASE=1
make STATIC=1
```
Strip the file to make it smaller, then relocate it:
```
strip compoundd
sudo cp compoundd /usr/bin
```
Now run the daemon:
```
compoundd
```
It should return an error, telling you to set up config file in a directory. 

## Create a config file

Now we’ll set up the config file. Note that this is case sensitive.
```
Linux
nano ~/.Compound/Compound.conf
Winodws
C:\Users\YourUserName\AppData\Roaming\Compound
```
Add the following, save and exit:
```
stake=1
listen=1
daemon=1
server=1
onlynet=ipv4
irc=1
splash=0
dns=1
rpcuser=(username)
rpcpassword=(strong password)
addnode=104.219.232.174
addnode=108.160.119.103
addnode=175.144.166.220
addnode=176.63.27.30
addnode=193.109.145.138
addnode=209.124.141.103
addnode=45.225.237.172
addnode=46.200.21.70
addnode=46.212.40.144
addnode=49.228.239.12
addnode=64.188.185.209
addnode=77.235.109.45
addnode=78.26.130.220
addnode=79.142.69.160
addnode=79.173.127.1
addnode=82.64.109.25
addnode=84.54.25.178
addnode=89.166.46.248
addnode=93.176.148.124
```
Run compoundd once more and if you did everything correctly, your daemon is now online! 
## Command summary
Type:
```
help
```
for a full list of commands available.
## Attention!!!
Do not keep more than 90,000,000,000 COMP coins in your wallet.
More than 90,000,000,000 coins becomes a negative balance.
If you are lucky enough to have that much start a second wallet on another computer.

