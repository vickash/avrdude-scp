#avrdude-scp

A shell script that automates the process of copying a compiled .hex file to a remote host and uploading it to an attached Arduino. Useful for uploading new code to Arduinos attached to OpenWrt routers, or any other *nix machine.

## Requirements

* SSH access to the remote machine
* `avrdude` installed on the remote machine
* .hex file compiled locally
* Arduino board attached to remote machine

## Usage

```shell
avrdude-scp user@host /dev/ttyACM0 my_sketch.hex
```

Replace `/dev/ttyACM0` with the device your Arduino is on the remote.

## Limitations

For now `avrdude` assumes the Arduino programmer and ATMega328p chip.
