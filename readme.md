# avrdude-scp

A shell script wrapper for `avrdude` and `scp` that automates the steps to copy a compiled .hex file to a remote machine and upload it to an Arduino / AVR attached to that machine. Useful for upadating code on Arduinos attached to OpenWrt routers, Raspberry Pis or any other *nix machine.

The remaining `avrdude` [functionality](http://www.nongnu.org/avrdude/user-manual/avrdude_4.html), should work too.

## Requirements

* SSH access to remote machine
* `avrdude` installed on remote machine
* Arduino / AVR microcontroller attached to remote machine
* Compiled .hex file on local machine

## Usage

Works just like `avrdude` except the `-P` option can take an 'scp-style' path like `user@host:/dev/device_to_flash`.

A `--retry N` option can be given to avrdude-scp to retry the requested command N times before giving up and deleting the image from the remote host.

Additional commands can be run before and after executing avrdude with the `--pre` and `--post` options. Several commands can be executed if they are separated by a semicolon. This can be used to stop and restart processes communicating with the microcontroller through the programmers serial port.

## Examples

Upload local file "blink.hex" to an Arduino UNO attached to a Raspberry Pi over the network:
```shell
avrdude-scp -V -F -c arduino -p m328p -P pi@raspberry:/dev/ttyACM0 -U flash:w:blink.hex
```

Dump the flash memory from the remote UNO to a local file, "dump.hex":
```shell
avrdude-scp -V -F -c arduino -p m328p -P pi@raspberry:/dev/ttyACM0 -U flash:r:dump.hex:r
```

Retry the averdude command 3 times, if it fails:
```shell
avrdude-scp -V -F -c arduino -p m328p -P pi@raspberry:/dev/ttyACM0 -U flash:w:blink.hex --retry 3
```

Executing a command on the remote host before and after avrdude:
```shell
avrdude-scp -V -F -c arduino -p m328p -P pi@raspberry:/dev/ttyACM0 -U flash:r:dump.hex:r --pre "date; ls -l" --post date
```

__Note__: The `-U` option works with local file paths, not files on the remote machine. The script handles the copying and cleanup.
