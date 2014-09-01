#avrdude-scp

A shell script wrapper for `avrdude` and `scp` that automates the steps to copy a compiled .hex file to a remote machine and upload it to an Arduino / AVR attached to that machine. Useful for upadating code on Arduinos attached to OpenWrt routers, Raspberry Pis or any other *nix machine.

The remaining `avrdude` [functionality](http://www.nongnu.org/avrdude/user-manual/avrdude_4.html), should work as expected too. Except for interactive mode, `-t`.

## Requirements

* SSH access to remote machine
* `avrdude` installed on remote machine
* Arduino / AVR microcontroller attached to remote machine
* Compiled .hex file on local machine

## Usage

Works just like `avrdude` except the `-P` option can take an `scp` style path like `user@host:/dev/device_to_flash`.

__Example:__
```shell
avrdude-scp -V -F -c arduino -p m328p -P user@host:/dev/ttyACM0 -U flash:w:blink.hex
```

__Note__: The `-U` option only takes a file that exists on your local machine, not the remote. The script handles all the `scp` business.
