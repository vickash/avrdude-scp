#avrdude-scp

A shell script that automates the process of copying a compiled .hex file to a remote host and uploading it to an attached Arduino. Useful for uploading new code to Arduinos attached to OpenWrt routers, or any other *nix machine.

## Requirements

* SSH access to the remote machine
* `avrdude` installed on the remote machine
* .hex file compiled locally
* Arduino board attached to remote machine

## Usage

Works just like `avrdude` except the `-P` option can take an `scp` style path like `user@host:/dev/device_to_flash`.

__Example:__
```shell
avrdude-scp -V -F -c arduino -p m328p -P user@host:/dev/ttyACM0 -U flash:w:du.hex
```

__Note__: You must give the path to a local file in the `-U` option. The script handles all the `scp` business.
