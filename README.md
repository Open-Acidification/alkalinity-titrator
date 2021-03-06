# Alkalinity Titrator Project
## Project motivations
As CO2 levels increase, the ocean absorbs more CO2 and becomes more acidic. There currently exists a large deficit of data on how this affects wildlife. Alkalinity Titrators are needed for ocean acidification research​. Currently, available models are  expensive ($10,000-$25,000)​. Models on the lower end of the price range are not automated and are therefore time intensive.

This project aims to make ocean acidification research more widely available by lowering the cost of alkalinity titrators. 

The problems that the alkalinity-titrator seek to fix are as follows:
- Lower the cost of ocean science equipment by using inexpensive, widely-available parts
- To automate the titration process, saving time and effort when determining total alkalinity

The titration process used in this project is based on SOP 3b from

```Christian, James Robert, Andrew G. Dickson, and Christopher L. Sabine. Guide to Best Practices for Ocean CO2 Measurements. Sidney, B.C.: North Pacific Marine Science Organization, 2007.``` 

## Setup and Installation
### Setting up the Raspberry Pi
Refer to https://desertbot.io/blog/headless-raspberry-pi-3-bplus-ssh-wifi-setup for instructions on setting up the raspberry pi (note: headless setup is not required if a keyboard and monitor are available). Raspbian lite has everything needed, but the desktop version can be downloaded if working with a GUI is preferable. 
### Installing software
Run standard updates on the pi:
``` 
$ sudo apt-get update 
$ sudo apt-get upgrade
```
This project utilizes SPI and I2C protocols, both of which often come disabled on the pi. To enable them, run:
```
$ sudo raspi-config
```
and navigate to "Interfacing Options"; enable both SPI and I2C.

Install git:
```
$ sudo apt-get install git
```
Clone alkalinity titrator repository to the pi
```
$ git clone https://github.com/Open-Acidification/alkalinity-titrator.git
```
Run installation script
```
$ sudo ./install.sh
```

## User Instructions
Run script
``` 
$ ./run.sh
```
Follow the user prompts and you're good to go!

## Pins
### Temperature probe ([MAX31865 breakout board](https://learn.adafruit.com/adafruit-max31865-rtd-pt100-amplifier/python-circuitpython))
- PIN 1 (3.3v) to sensor VIN
- PIN 9 to sensor GND
- PIN 19/BCM 10 to sensor SDI
- PIN 21/BCM 21 to sensor SDO
- PIN 23/BCM 23 to sensor CLK
- PIN 29/BCM 5 to sensor CS (or use any other free GPIO pin)

### pH probe ([ADS1115 analog converter](https://learn.adafruit.com/adafruit-4-channel-adc-breakouts/python-circuitpython))
- PIN 17 (3.3v) to ADS1115 VDD - Remember the maximum input voltage to any ADC channel cannot exceed this VDD 3V value!
- PIN 6 to ADS1115 GND
- PIN 5/BCM 3 SCL to ADS1115 SCL
- PIN 3/BCM 2 to ADS1115 SDA

## Libraries
1. Circuit Python - https://github.com/adafruit/Adafruit_CircuitPython_MAX31865 
<br>
Used for communicating with the PT1000 