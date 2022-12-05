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
