#avrdude-scp

A shell script that automates the process of copying a compiled .hex file to a remote host and uploading it to an attached Arduino. Useful for uploading new code to Arduinos attached to OpenWrt routers, or any other *nix machine.

## Usage

```shell
# Replace /dev/ttyACM0 with the device the Arduino is attached to on the remote.
avrdude-scp user@host /dev/ttyACM0 my_sketch.hex
```

## Limitations

For now `avrdude` assumes the Arduino programmer and ATMega328p chip.
