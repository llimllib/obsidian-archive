---
created: 2025-10-27T12:35:03.305Z
updated: 2025-10-27T12:35:03.305Z
---
I'm annoyed by the bright LED on my Logitech g203 mouse, but I also refuse to install Logitech drivers which are consistently awful, so I had just accepted that I'd have to be annoyed by it.

Until today! I got annoyed enough that I looked around and found out that somebody already figured out how to do it, and with a little tweaking I was able to use their solution on my mac to disable the LED without installing a driver.

Here's what I ended up with after a few minutes of hacking:

- Install libusb: `brew install libusb`
- clone [smasty/g203-led](https://github.com/smasty/g203-led/tree/master) and cd into `g203-led`
- edit `requirements.txt` to upgrade the `pyusb` version to 2.3.1
- `pip install -r requirements.txt` to install pyusb
- `sudo python g203-led.py lightsync solid 000000`

That's it! Thank you very much to the open source goblins who figured this out.