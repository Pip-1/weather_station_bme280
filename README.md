### Setup Raspberry  Pi
Headless Setup of a Raspbery Pi Zero W:
[Lutz's Tutorial on headless Setup](https://www.youtube.com/watch?v=hoy4x7MTA-o)

[Imager from the Raspberry Pi Manufacturer](https://www.raspberrypi.com/software/) with which i mounted the default Raspi OS on an SD Card

including finding out about your raspis IP-Adress with
    ping -4 raspberrypi

You can transfer files easy via SCP::

    scp <source-file> <user>@<host_ip_address>:<path>
    
    



### Update Pi
     sudo apt-get update
     sudo apt-get install -y python3 python3-dev python3-pip git sqlite3 

     
### Offline Setup of the BME280 to the Raspberry Pi Zero
First you will have to solder the pins to the pcb of the bme280.

Then connect the bme280 to the raspberry Pi Board with the help of jumper cables.

| BME280-Pin | Pin on RaspberryPi |
| --- | --- |
| GND | GND |
| VIN | 3V3 |
| SCL | GPIO3 |
| SDA | GPIO2 |


### Get BME280 running

[Link from Matt Hawkins](https://www.raspberrypi-spy.co.uk/2016/07/using-bme280-i2c-temperature-pressure-sensor-in-python/) to get BME280 from AZ-Delivery running <br>
or <br>
download the python script from your raspi console:
     
    wget -O bme280.py http://bit.ly/bme280py

Running this script via
     python bme280.py
should output a few nice print statements.

Inside of this function, the sensor data is being extracted and transformed from a raw output and passed on as understandable and handable variables: *temperature, humidity, pressure*


PS: There is also a [manual of AZ-Delivery](https://www.az-delivery.de/products/gy-bme280-kostenfreies-e-book?variant=19134838997088) themselves on this sensor. You can download it for free.


### Installing peewee for ORM Setup of a Database
The [Documentation of peewee is very nice!](http://docs.peewee-orm.com/en/latest/)
#### Install:
     sudo pip3 install peewee

#### Usage:
     sudo python3 bme_read.py

hint: look into model.py


### Setup Database with the Help of peewee:


#### Settinn up Database with SQLite3
actually creating a new db in the current dir <br>
     sqlite3 dht.db
     
creating some tables:
    CREATE TABLE readings (time DATETIME, sensor TEXT, temperature REAL, humidity REAL, pressure REAL);
    
    
#### Creating a Service on Linux/Raspberry Pi
[How to from toms hardware under:](https://www.tomshardware.com/how-to/run-long-running-scripts-raspberry-pi)
     
## Old Notes
## Raspberry Pi weather station

The goal of this project is a very simple raspberry pi weather station. It will be accessable via a Telegram bot.
We will see.

There are endless possibilities of using a Raspberry Pi as a weather station. Feel free to try them all!
## Setup

#### Rasperry Pi
- used or new, i.e.: i got all my Pi's from ebay-Kleinanzeigen for a small buck
- i will take a Rasperry Pi Zero W V1.1, but every other Pi will work just as well

#### SD-Card
- the storage unit is needed for the image of the OS the Raspberry Pi will run with
- i got 32 GB, 8 GB will be sufficient enough for most OS, though
- with a script, you could easily store the weather data in various files on the SD-Card as well
- keep in mind, that a high number writing processes will shorten the life span of your card drastically

#### Bosch GY-BME280
- barometric sensor for temperature, humidity and air pressure
- i got one from AZ-Delivery, but there are different manufacturers using the BME280

- there are different sensors you could use for this task, another option could be DHT11 or DHT22

#### Tools and Equipment

#### Soldering Iron
- soldering iron is very useful for the connection of the pins from either the sensor or pi to the pcb's
- i think you can build this without the need of soldering, just need to be a bit creative (hit me up for tips and tricks)
  

## Process

#### Raspberry Pi Setup

- we will do a headless setup, meaning we won't have to connect the Pi to any peripherals other then the power cord
- the OS will be put on the SD-card with the help of the [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
- there is two files in this repository you will need to add, to the SD-cards folder "Boot" (it's just the main folder):
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **wpa_supplicant.conf** - this is a simple text file containing the log-in info to the wifi
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **ssh** - this is a simple and **empty** text file, which activates the SSH-Protocoll, so we can remotely controll the Pi later on
- after the OS is on the card and both files have been added to the folder, we can insert the card it into the Pi, plug it in and let it boot up

**SSH connection**
- there is different ways of checking, if your Pi logged into your network (accessing router via browser)
- let's open the terminal and check for the ping:
''' ping raspberrypi
>>>Ping wird ausgeführt für raspberrypi.fritz.box [2a02:2454:95ac:1600:b95:6f1f:d2dc:9710] mit 32 Bytes Daten:
>>>Antwort von 2a02:2454:95ac:1600:b95:6f1f:d2dc:9710: Zeit=73ms
>>>Antwort von 2a02:2454:95ac:1600:b95:6f1f:d2dc:9710: Zeit=5ms
'''

- perfect, let's connect:
''' ssh pi@raspberrypi
>>> The authenticity of host 'raspberrypi (---)' can't be established.
>>> ECDSA key fingerprint is ---.
>>> Are you sure you want to continue connecting (yes/no/[fingerprint])?
yes
>>> Warning: Permanently added 'raspberrypi,2a02:2454:95ac:1600:b95:6f1f:d2dc:9710' (ECDSA) to the list of known hosts.
>>> pi@raspberrypi's password:
**enter password here** hint: default password of the pi is "raspberry")
- now you should be connected to the terminal of your pi
- to update your pi, which probably won't be necessary, you could get root permission with '''sudo su-'''
- update everything with '''apt-get update'''
- upgrade everything with '''apt-get upgrade'''
- 

