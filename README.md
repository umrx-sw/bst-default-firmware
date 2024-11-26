# BST Default firmware

(**Unofficial**) Default BST firmware for [Application Board 3.1](https://www.bosch-sensortec.com/software-tools/tools/application-board-3-1/) or 
[3.0](https://www.bosch-sensortec.com/software-tools/tools/application-board-3-0/) hardware.

The boards are shipped pre-programmed with the firmware.

If you would like to restore the firmware to its default state
(possibly after some experimentation), 
here you can find the HEX files for programming.

## Program the board

1. Go to the [release page](https://github.com/umrx-sw/bst-default-firmware/releases) and download the `*.hex` files.

2. install the `nrfjprog` tool which is part of 
[nRF-Command-Line-Tools](https://www.nordicsemi.com/Products/Development-tools/nRF-Command-Line-Tools/).
The `nrfutil` tool seems to have similar functionality, but reading and writing the memory addresses 
does not work.

3. Connect debugger to the SWD interface of the board and power ON the board

4. Program the firmware

  4.1. For Application Board 3.1, run

```bash
nrfjprog -f nrf52 --program application_board_v3_rev1_fw.hex --sectorerase --verify
```

  4.2. For Application Board 3.0, run:

```bash
nrfjprog -f nrf52 --program application_board_v3_rev0_fw.hex --sectorerase --verify
```

5. Write the bootloader address to the (`UICR.BOOTLOADERADDR`, `0x10001014` in the reference manual: `UICR.NRFFW[0]`):

```bash
nrfjprog -f nrf52 --memwr 0x10001014 --val 0x000F0000
```

