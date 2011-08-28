# Launchpad - Processing Library to control Novation Launchpad

This library provides an interface to access [novation's launchpad](http://www.novationmusic.com/products/launchpad) programmatically. 
It's based on Thomas Jachmanns [ruby launchpad gem](http://github.com/thomasjachmann/launchpad). LEDs can be lighted and button presses can be listened to. In addition, it includes a wrapper for the [Monomic Library](http://jkriss.github.com/monomic) as well.


## Requirements

  * Severin Smiths [themidibus library](http://smallbutdigital.com/themidibus.php)
  * On Mac OS X < Java Update 6 you need Humatics [mmj library](http://www.humatic.de/htools/mmj.htm) as well. Yes, go and spend those 3.5 - it's worth it!
  * obviously a Novation Launchpad ;-)

## Installation

Download, unzip and put the extracted launchpad folder into the libraries folder of your processing sketches. Reference and examples are included in the launchpad folder.
If needed (only Mac OS X with java Update < 6), install *mmj* library as described in their documentation.


## Usage

Basically, create an instance of the Launchpad class and your're ready to go. This is a simple example that switches on all LEDs (for testing), resets the launchpad again and then lights the grid button at position 4/4 (from top left).

    import themidibus.*;
    import com.rngtng.launchpad.*;

    Launchpad device;

    void setup() {
      device = new Launchpad(this);
      noLoop();
    }

    void draw() {
      device.testLeds();
      delay(1000);
      device.reset();
      delay(1000);
      device.changeGrid( 4, 4, LColor.RED_HIGH + LColor.GREEN_LOW);
    }

For Interaction, make sure to include Pressed/Released Listener for grid, the button on the top and scene buttons on the right. This is an interaction example lighting all grid buttons in red when pressed and keeping them lit.

    import themidibus.*;
    import com.rngtng.launchpad.*;

    Launchpad device;

    void setup() {
      device = new Launchpad(this);
      noLoop();
    }

    void draw() {
    }

    void launchpadGridPressed(int x, int y) {
      device.changeGrid( x, y, LColor.RED_HIGH);
    }

    void launchpadButtonPressed(int buttonCode) {
      if(buttonCode == LButton.MIXER) exit();
    }


For more details, see the examples. Most examples are ported from the ruby and monomic library

## Near future plans

  * add proper Exception/Warning handling
  * use entities instead of Consts??
  * add test (how to do this with processing??)


## Contributors

  * [AspeteRakete](https://github.com/aspeteRakete): [Pullrequest #1](https://github.com/rngtng/launchpad/pull/1)

Big Thank you!

## Changelog

### v0.3

  * Merged [Pullrequest #1](https://github.com/rngtng/launchpad/pull/1), to bee up to date with external libs
  * Included external libs
  * Updated build file & Website

###  v0.2.2

  * bugfixes
  * added connected() method


###  v0.2.0

  * interaction fully working, accepts PApplet or custom Listeners
  * first stable version, API is nearly fixed now
  * nice color handling using the LColor class
  * monomic wrapper class
  * lots of new examples
  * proper buffer & flashing support

###  v0.1.0

  * first version, supporting output only




## Copyright
The MIT License

Copyright © 2011 RngTng, Tobias Bielohlawek

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.