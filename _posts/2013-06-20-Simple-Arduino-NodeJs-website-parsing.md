---
layout: post
category: Blog
tags: [Arduino, NodeJs]
title: "Making a simple web data monitor with Arduino + NodeJs"
---
The idea behind this project was to have some almost-real-time website information available at glance on of my desk in a sort of a really simplified dashboard. At it turned out pretty straight forward using NodeJs to fetch the website and do all the data parsing needed and then sending the data thru USB to an Arduino board with a LCD shield on it.

## Components needed

* Arduino board (UNO compatible), I got mine at [dx.com](http://dx.com)
* LCD shield. Also bought it from dx but if you are going to get one now there are other Arduino-compatible LCD modules that only require a couple of pins to make the screen work, mine unfortunately uses almost 6 or 7, not cool.
* Usb cable

And that's all the fancy hardware we are going to need, as i said before this is a simple quick prototype but the hardware and software can be used as a starting point to have this working over a bluetooth connection or setting up more interaction points so every time you wave in front of the screen you could get the next tweet on your timeline displayed, when designing things with Arduino + internet stuff the sky is the limit (not really but it sounds really good).


## The NodeJs brains

The script is composed of two stages, first we need to get the webpage and get out the data we need and second we need to format the data so when we send it over the serial connection to the Arduino it can display it properly.

This example gets the current argentinian peso exchange value for usd dollar and euros every 30 minutes.

<div class="highlight-gist">
<div class="code">
{% gist 5820493 %}
</div>
</div>

As you can see the code is quite tailored for this specific example, specially the padding and data formatting part.

## Arduino's silly job, just displaying strings

As I mentioned before the board is programmed to show whatever the serial connection brings to it, reducing the logic on the Arduino side to nearly zero.


<div class="highlight-gist">
<div class="code">
{% gist 5794749 %}
</div>
</div>

## Some assembly needed

So, this is the hard part, the assembling of our electronics project, follow the steps:

1. Take the LCD shield and place it onto the Arduino making sure all connector are in place
2. Plug the USB cable to you pc/mac/toaster and the other end to the Arduino board
3. Load the arduino code using the provided IDE
4. Fire up the node script `node parse.js` in the console
5. Profit

![Project working](http://f.cl.ly/items/463c3f393s401m1Z3d04/arduino-nodejs-webpage-parser.jpg "Project completed")
