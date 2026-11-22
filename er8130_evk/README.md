# ESMT ER8130 EVK for Arduino

Arduino support for the ESMT ER8130A / ER8131A Sub-1GHz radio SoC on the
ER8130 EVK. Windows only.

## Install

1. In the Arduino IDE open *File > Preferences* and add this to
   *Additional boards manager URLs*:

   ```text
   https://github.com/KWYangESMT/ESMT-Arduino/raw/refs/heads/main/er8130_evk/package_esmt_index.json
   ```

2. Open *Tools > Board > Boards Manager*, search for **ESMT** and install
   *ESMT ER813x Boards*. The IDE also downloads the Arm GNU Toolchain
   13.3.Rel1 from Arm (about 300 MB). Python is not needed. If the download
   times out, close the IDE, add this to `C:\Users\<name>\.arduinoIDE\arduino-cli.yaml`
   and install again:

   ```yaml
   network:
     connection_timeout: 1800s
   ```
3. Select *Tools > Board > ESMT ER813x Boards > ESMT ER8130 EVK* and the
   board's COM port.

## Upload

The board must have the Arduino loader in flash. Boards are delivered with it.

Press *Upload*. The uploader resets the running sketch over the serial port
and writes the new sketch through the loader, so no reset wiring is needed.
If the upload cannot reach the loader, for example because the sketch was
built with *Tools > Watchdog > Off* and is stuck, press the board's reset
button when the uploader asks. The loader listens for an upload for 0.5 s
after a reset, then starts the sketch.

`Serial` is the USB serial port (UART0) at 115200 8N1 by default.

## Board menu

- *Watchdog*: 2 s (default), 8 s or Off. The core feeds the watchdog on every
  `loop()` pass and in `delay()`. A sketch that blocks for about twice the
  timeout is reset, which keeps uploads working with a stuck sketch.
- *Debug*: Off (default) or On (`-g`).

## EVK pins

| Pin | Use |
|---|---|
| GPIO2, GPIO3 | LEDs (`LED_BUILTIN` is GPIO2) |
| GPIO13 | Button |
| GPIO5, 6, 7, 8 | Free; default SPI SCK, MOSI, MISO, SS |
| GPIO11, GPIO12 | Free; default Wire SDA, SCL (external pull-ups needed) |
| GPIO10 | Free; default Serial1 TX (Serial1 RX is GPIO8, shared with SS) |
| A0 | Analog input (dedicated pin, not a GPIO); A1 battery, A2 temperature |

GPIO4 and GPIO9 are not available. `analogWrite()` and `tone()` work on any
free GPIO, up to 6 PWM pins at once. `SPI.setPins()`, `Wire.setPins()` and
`Serial1.setPins()` before `begin()` move a bus to other pins.

## Libraries

Included: SPI, Wire (master and slave), EEPROM, ESMTLowPower (the
ArduinoLowPower API), ESMTRadio (GFSK packet radio, an API like the LoRa
library), ESMTTimer (the TimerOne API). Each has examples under
*File > Examples*.

Many libraries written for AVR boards also work: `<avr/pgmspace.h>`,
`dtostrf()`, `<util/delay.h>` and `sei()` / `cli()` are provided, and C++ is
built with `-fpermissive` as on the AVR core. Code that uses AVR registers or
`ISR()` vectors does not work.

## Known limitations

- `Wire.endTransmission()` returns 0 even when the device does not answer a
  write with data. An address check with no data (as in I2CScanner) does
  report a missing device.
- Each Wire transfer takes at least about 1 ms.
- Wire slave: a write to the board takes about 70 ms, and a reply after a
  repeated START starts with a byte prepared before the write. Use a STOP
  between the write and the read.
- ESMTRadio: a send can fail after the radio has been receiving, after a
  frequency change or after a TX power change.
- `LowPower.sleep(ms)` can last about 15 % longer than requested.
- A sleeping board cannot be reset by the uploader: keep timed sleeps short
  while developing, or press reset.
