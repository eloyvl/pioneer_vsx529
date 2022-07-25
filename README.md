# Async Pioneer VSX-529

My VSX-529 AV amp is not working with the original Home Assistant Pioneer driver.
After some changes on the original driver it worked for a few hours, a day or two at max only. After that it freezes, and only a power off/on cycle makes it useable again.
This is because that driver creates a new telnet connection to the amp for every update, it queries the required info, and then closes the connection. The telnet software in the amp firmware probably has memory leak, that might be the reason for this freeze after a few thousands of telnet connections.

No firmware updates available for this amp anymore.

I found the work of [realthk](https://github.com/realthk) who did a amazing work for his Pioneer AV.
His AV has much more functions and didn't fit to my one.

So I took his async approach and merged it with the original HASS Pioneer driver.

The Pioneer VSX-529 is not supporting the Volume Set function so I added Volume Step Support.
Additional I build a small control loop for the Volume Set function. It is now possible to set a volume level directly. Please keep in mind, that this is not a perfect control loop, so use this function carefull!

## Install

1. Download and copy [media_player.py](https://github.com/SpaceMaster85/pioneer_vsx529/blob/master/media_player.py) and [init.py](https://github.com/SpaceMaster85/pioneer_vsx529/blob/master/__init__.py) into `config/custom_components/pioneer_vsx529` directory.

2. Add a reference to this inside your `configuration.yaml`:

  ```yaml
media_player:
- platform: pioneer_vsx529
  host: 192.168.1.34
  port: 8102
  name: Pioneer VSX-529
  sources:
    'CD' : '01'
    'FM tuner' : '02'
    'DVD' : '04'
    'TV' : '05'
    'SAT/CBL' : '06'
    'No Device' : '17'
    'HDMI' : '19'
    'BD' : '25'
    'ADP' : '33'
    'Net Radio' : '38'
    'M Server' : '44'
    'Favorite' : '45'
    'MHL' : '48'
    'Game' : '49'
  ```
  
  This verison needs Home Assistant v.0.110 or higher! For the previous version plese see the coresponding branch.

