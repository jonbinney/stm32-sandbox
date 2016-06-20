## Setting up the tools

Install dependencies.

```
sudo apt-get install gcc-arm-none-eabi
sudo apt-get install binutils-arm-none-eabi
sudo apt-get install gdb-arm-none-eabi
sudo apt-get install libusb-1.0-0-dev
```

Clone and build libopencm3-examples (which includes libopencm3 as a submodule).

```
git clone --recursive git@github.com:libopencm3/libopencm3-examples
cd libopencm3-examples
make
```

Clone and build st-link.

```
git clone git@github.com:texane/stlink
mkdir stlink-build
cd stlink-build
cmake ../stlink
make
```

## Running/flashing code
For some reason flashing fails with `st-util` unless I run it with
`-v`. See https://github.com/texane/stlink/issues/182

In one terminal, run the st-util server.
```
st-util -v
```

In a second terminal, run the gdb client, connect to the server, and
load/flash then run the code.

```
cd examples/stm32/f0/stm32f0-discovery/miniblink
arm-none-eabi-gdb miniblink.elf
tar extended-remote :4242
load
continue
```

If it works, an LED (LD4) on the board should flash.

