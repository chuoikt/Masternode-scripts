# Pentanode
Shell script to install a [Pentanode Masternode](https://bitcointalk.org/index.php?topic=???? ) on a Linux server running Ubuntu 16.04. Use it on your own risk.  
***

## Installation for v1.1.0.1-60010:
```
wget -q https://raw.githubusercontent.com/PentaNode/Masternode/master/pentanode.sh
bash pentanode.sh
```
***

## Desktop wallet setup  

After the MN is up and running, you need to configure the desktop wallet accordingly. Here are the steps:  
1. Open the Pentanode Desktop Wallet.  
2. Go to RECEIVE and create a New Address: **MN1**  
3. Send **2500** **5000** **10000** **15000** or **25000** PTN to **MN1**.
4. Wait for 15 confirmations.  
5. Go to **Help -> "Debug Window - Console"**  
6. Type the following command: **masternode outputs**  
7. Go to **Masternodes** tab  
8. Click **Create** and fill the details:  
* Alias: **MN1**  
* Address: **VPS_IP:PORT**  
* Privkey: **Value given during VPS Setup**  
* TxHash: **First value from Step 6**  
* Output index:  **Second value from Step 6**  
* Reward address: leave blank or fill with PTN address of your choice 
* Reward %: leave blank or fill with the percentage of your choice
9. Click **OK** to add the masternode  
10. Click **Update**  
10. Click **Start All**  
***

## Multiple MN on one VPS:

It is now possible to run multiple **Pentanode** Master Nodes on the same VPS. Each MN will run under a different user you will choose during installation.  
***

## Usage:

For security reasons **Pentanode** is installed under a normal user, usually **pentanode**, hence you need to **su - pentanode** before checking:  
```
PENTAUSER=pentanode #replace pentanode with the MN username you want to check  
su - $PENTAUSER
PentaNoded masternode status  
PentaNoded getinfo
```
Also, if you want to check/start/stop **pentanode** daemon for a particular MN, run one of the following commands as **root**:
```
PENTAUSER=pentanode  #replace pentanode with the MN username you want to check  
systemctl status $PENTAUSER #To check the service is running  
systemctl start $PENTAUSER #To start PentaNoded service  
systemctl stop $PENTAUSER #To stop PentaNoded service  
systemctl is-enabled $PENTAUSER #To check PentaNoded service is enabled on boot  
```
***

## Wallet re-sync

If you need to resync the wallet, run the following commands as **root**:
```
PENTAUSER=pentanode  #replace pentanode with the MN username you want to resync
systemctl stop $PENTAUSER
rm -r /home/$PENTAUSER/.PentaNoded/{banlist.dat,blk0001.dat,database,db.log,mncache.dat,peers.dat,smsgDB,smsg.ini,txleveldb}
systemctl start $PENTAUSER
```
***
