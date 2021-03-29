
# Componets #

**Register Select** (RS, 


## Serial 1 ##

Serial 1 is the USB port of the board.


## Serials ##

| BOARD | PORT | RX | TX |
| -- | -- | -- | -- |
| MEGA | D | 19 | 18 |
| UNO | D | 0 | 1 |


## Set the direction register ##

```c
// set pins 8..13 as output...
DDRB = B00111111;  // digital pins -,-,13,12,11,10,9,8
        
DDRB |= B00000100;        //Sets D10 as OUTPUT
DDRB &= B00000100;
```

```c
// Write simultaneously to pins 8..13...
PORTB = B00111000;   // turns on 13,12,11; turns off 10,9,8
```        

## SPI ##

### Chip Select ###

[Ref 1](https://learn.sparkfun.com/tutorials/serial-peripheral-interface-spi/chip-select-cs)

Each device has its own CS line/pin. When the pin is high the device is not active and when low the device will activate and will send or receive data.

To talk to a particular peripheral, you'll make that peripheral's CS line low and keep the rest of them high.

# References #

[Tutorial 1](https://electronoobs.com/eng_arduino_tut130.php)
