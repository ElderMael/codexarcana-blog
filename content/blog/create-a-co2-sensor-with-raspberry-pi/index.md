---
title: "Building A Web Service For A CO2 Sensor With A Raspberry Pi"
description: "An illustrated guide to use a CCS811 sensor with Raspberry Pi"
date: "2020-11-19T19:53:28-06:00"
categories: 
  - IoT
  - Grafana
  - Prometheus
  - CCS811

published: true
canonical_link: https://blog.eldermael.io/co2-sensor-raspberry-pi
redirect_from:
  - /co2-sensor-raspberry-pi
---

I recently wanted to introduce my daughters to the programming, so I decided
to use some kind of sensor to prototype a small application and teach them
how to make hardware and software work in tandem as I believe having something
physical would be more interesting than me typing on a REPL.

Now, I knew a raspberry pi had a way to connect sensors using its [General-purpose
input/output][1] pins, so I decided to build a non-trivial application to 
get used to the programming model and at the same time have experience to build 
something more complex later.

## Hardware Required

To start the project I did some research for sensors and while there were quite a
bit of choices, I got interested in the [KeyEstudio CCS811 Carbon Dioxide/ Air Quality 
Sensor for Arduino][2] which is compatible with Raspberry Pi 5V pins. It also works 
using the [I²C communication bus][3] which is also supported.

Now, in order to prototype faster, I got a [T-type breakout, a solderless board, and
rainbow cable, plus jump wires][4]. With this at hand, I was able to start interfacing 
the GPIO with the sensor.

## Wiring It All Together

Now, it was a while (since my college days) that I had work on a solderless board but
fortunately there is a diagram to connect the sensor to an arduino board thus you
can deduce how to wire it to the equivalent pins on a Raspberry Pi.

![](./sensor-connection.png)

With this diagram, and the official Raspberry Pi documentation, I was able to find the
correct pins without much issue. For reference, here is the Raspberry Pi GPIO pin
diagram (this is for Raspberry Pi 4 Model B).

![](./gpio-pins.png)

Finally, with the help of the T-type breakout, and the solderless board, here is a picture
of the connections. Note that the breakout already labels the pins so is not hard
to match them.

![](./solderless-board-connections.jpeg)

## Validate Connections Through Raspberry Pi and i2cdetect

Now, with everything wired, the fastest way to detect if the sensor is properly interfacing
to the I²C bus is to run a utility which can be installed on the Raspberry Pi Os named
[`i2cdetect`][5]. Here is the command:

```shell script

pi@elderserver:~ $ i2cdetect -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- 5a -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --

```

[1]: (https://en.wikipedia.org/wiki/General-purpose_input/output
[2]: https://www.keyestudio.com/keyestudio-ccs811-carbon-dioxide-temperature-air-quality-sensor-for-arduino-p0581.html
[3]: https://en.wikipedia.org/wiki/I%C2%B2C
[4]: https://www.amazon.com/gp/product/B07DL25MVQ/ref=ppx_yo_dt_b_asin_title_o05_s02?ie=UTF8&psc=1
[5]: https://linux.die.net/man/8/i2cdetect