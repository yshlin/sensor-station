SensorWeb Station
==============
SensorWeb Station software/firmware for various devboards.

## Setting Up Your PM Sensor Station with RPi


### Hardware Requirements:

* Raspberry Pi (currently only tested with RPi 2)
* At least 4G SDCard
* Plantower PM Sensor (currently only tested with PMS3003) with Cable

### Setup Steps

#### 1. Prepare OS

[Install Raspbian on Your SDCard.](https://www.raspberrypi.org/documentation/installation/installing-images/)

Insert the SDCard to your RPi when done.

#### 2. Connecting Sensors

You only need to connect 4 pins of the PM Sensor, others should be left unconnected.

PM Sensor Pins| RPi Pins
---------- | ----------
VCC (PIN1) | +5V (PIN2)
GND (PIN2) | GND (PIN6)
RXD (PIN4) | TXD (PIN8)
TXD (PIN5)| RXD (PIN10)


#### 3. Accessing and Configuring RPi

Power on your RPi and get access to it. 

It would be easier if you have screen/mouse/keyboard to access GUI. But if you prefer command line access, you can use a [USB to TTL cable](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable) or [SSH](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-6-using-ssh) when you got it's IP address. Note that USB to TTL cable uses serial pins, so you might need to unplug serial sensors first.

In order to read data from serial PM sensor, you'll have to disable serial console access first.  
```
sudo raspi-config
```  
Select 'Advanced Options' -> 'Serial' -> 'No'

#### 4. Setup and Run

Firstly, clone sensor station repository into your RPi:  
```
git clone https://github.com/yshlin/sensorweb-station.git
```

Change to the RPi implementation directory:  
```
cd sensorweb-station/RPi
```

Install dependencies:  
```
sudo pip install -r requirements.txt
```

Start the server, you'll see console output if it runs correctly:  
```
sudo python sensor_daemon.py
```

Access the sensor dashboard in RPi's browser with following URL:  
http://localhost:5000

If you RPi have an IP, you can access it on other devices via IP.  

### More Options

You may need to [install GrovePi](http://www.dexterindustries.com/GrovePi/get-started-with-the-grovepi/setting-software/) in order to use Grove Modules.

#### Connect More Sensors

Currently supported sensors are:

* Plantower PM Sensor
* Grove Temperature & Humidity Sensor Pro
* Grove Dust Sensor
* Other Grove Analog Sensors

Connect your sensor, uncomment and edit corresponding code in ```senser_daemon.py``` to use them.

#### More Output Method

Currently supported output method:

* Console output
* Grove LCD RGB Backlight
* Grove Chainable RGB LED  

Connect your module, uncomment and edit corresponding code in ```senser_daemon.py``` to use them.

### Next Steps

* Post data to SensorWeb server
* Store data offline and sync when online
* Offline Charts/Analytics
* Support GPS modules/dongles
* Support more devboards
