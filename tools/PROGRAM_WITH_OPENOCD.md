Program with OpenOCD
====

## Program
```
/usr/bin/openocd -s /usr/share/openocd/scripts/ -f daplink.cfg -c 'init' -c 'halt' -c 'program nrf52810_xxaa.hex verify reset'
```
