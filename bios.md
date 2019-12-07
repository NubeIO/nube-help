# bios-testing

API docs

https://documenter.getpostman.com/view/670606/RWguwGk8?version=latest#c1d46c5b-cf1b-4916-9f24-288dd94bda1e

## Install

### to download the bios from nexus
http://45.63.30.129:8081/#browse/browse:raw:edge%2Fbios%2Fnubeio-edge-bios-1.0.0-SNAPSHOT-alpha.1%2Bb1.zip

### Install java

```shell
sudo apt-get update
sudo apt-get install openjdk-8-jre
```

## Fashing the PI compute

On your Linux PC

https://www.raspberrypi.org/documentation/hardware/computemodule/cm-emmc-flashing.md
```
sudo apt install git
mkdir usbboot
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
sudo apt install libusb-1.0-0-dev
make
sudo ./rpiboot

```
Then plugin the PI as a USB device into your PC and follow these steps

`Method 2: Easy Way`

https://raspberrypi.stackexchange.com/questions/96032/how-do-i-flash-install-raspbian-on-raspberry-pi-compute-module-3-3


## Update PI Password

https://www.raspberrypi.org/documentation/linux/usage/users.md

Once you're logged in as the pi user, it is highly advisable to use the passwd command to change the default password to improve your Pi's security.

Enter passwd on the command line and press Enter. You'll be prompted to

```
passwd
```




## Install node-red for testing end points
Its not required but you can import a flow for testing

https://nodered.org/docs/getting-started/raspberrypi

```shell
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)


Use   node-red-stop                          to stop Node-RED
Use   node-red-start                         to start Node-RED again
Use   node-red-log                           to view the recent log output
Use   sudo systemctl enable nodered.service  to autostart Node-RED at every boot
Use   sudo systemctl disable nodered.service to disable autostart on boot



```

#### Adding node-red password

https://nodered.org/docs/user-guide/runtime/securing-node-red

```
sudo npm install -g node-red-admin
node-red-admin hash-pw
cd /home/pi/.node-red
nano setting.js

```



## Running on a BBB

### Run with limits on memory

```shell
pi@raspberrypi:~/nubeio-edge-bios-1.0.0-SNAPSHOT-bacnet-alpha.09 $
sudo /usr/bin/java -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:+UseContainerSupport -XX:+UseSerialGC -XX:+TieredCompilation -XX:TieredStopAtLevel=1 -XX:MaxRAM=295m -XX:MinRAMPercentage=50.0 -XX:MaxRAMPercentage=80.0 -Xss256k -XX:ActiveProcessorCount=0 -Dvertx.blockedThreadCheckInterval=1 -Dvertx.blockedThreadCheckIntervalUnit=SECONDS -Dvertx.maxEventLoopExecuteTime=5 -Dvertx.maxEventLoopExecuteTimeUnit=SECONDS -Dvertx.maxWorkerExecuteTime=180 -Dvertx.maxWorkerExecuteTimeUnit=SECONDS -Dvertx.warningExceptionTime=5 -Dvertx.warningExceptionTimeUnit=SECONDS -jar nubeio-edge-bios-*.jar -conf bios.json

```

### Run with limits `no` memory
```shell
java -jar nube-edge-bios-*.jar -conf/bios.json
```

## Bios Config File

See in repo to download


## Updating

### Delete the DB file

```shell
sudo rm -rf /data/db/
```


### Upadting maven repo address

```shell
sed -i -e 's/nexus:8081/45.63.30.129:8081/g' bios.json 
```

## API examples

## Docs
https://documenter.getpostman.com/view/670606/RWguwGk8?version=latest#c1d46c5b-cf1b-4916-9f24-288dd94bda1e



### RQL Filters

```
http://127.0.0.1:8080/api/point?category=BACNET
http://127.0.0.1:8080/api/point?kind=input
```

```
Pretty: _pretty=true
Audit: _audit=true
Pagination: page=1&per_page=20
Sort: _sort=field1,+field2,-field3 | + or blank: ASC | -: DESC
Filter: field1=<value>&refTable.field1=<value>
```

### Points 

```
http://127.0.0.1:8080/api/point/edbe3acf-5fca-4672-b633-72aa73004917
http://127.0.0.1:8080/api/point/edbe3acf-5fca-4672-b633-72aa73004917/tags
http://127.0.0.1:8080/api/point/edbe3acf-5fca-4672-b633-72aa73004917/tags/3   //this is an valid ID
http://127.0.0.1:8080/api/point/edbe3acf-5fca-4672-b633-72aa73004917/data
http://127.0.0.1:8080/api/point/edbe3acf-5fca-4672-b633-72aa73004917/histories
http://127.0.0.1:8080/api/point/edbe3acf-5fca-4672-b633-72aa73004917/histories/5 //this is an valid ID
```


### services (These are like drivers in niagara)
```
http://127.0.0.1:8080/api/services
http://127.0.0.1:8080/api/services/com.nubeiot.edge.connector:bacnet
```


### modules (These are like services in niagara)
```
http://127.0.0.1:8080/api/modules
http://127.0.0.1:8080/api/modules/com.nubeiot.edge.module:datapoint
```


