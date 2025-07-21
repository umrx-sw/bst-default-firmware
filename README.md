# 🌟 BST Default firmware

(**Unofficial**) Default BST firmware for [Application Board 3.1](https://www.bosch-sensortec.com/software-tools/tools/application-board-3-1/) or 
[3.0](https://www.bosch-sensortec.com/software-tools/tools/application-board-3-0/) hardware.

The boards are shipped pre-programmed with the firmware.

If you would like to restore the firmware to its default state
(possibly after some experimentation), 
here you can find the HEX files for programming.

## 📖 How to program the board

1. Download the `*.hex` files from the [release page](https://github.com/umrx-sw/bst-default-firmware/releases).
   Alternatively, use `wget` to download the `*.hex` files:

For application board 3.0:
```bash
wget https://github.com/umrx-sw/bst-default-firmware/releases/latest/download/application_board_v3_rev0_fw.hex
```

For application board 3.1:
```bash
wget https://github.com/umrx-sw/bst-default-firmware/releases/latest/download/application_board_v3_rev1_fw.hex
```

2. Install the [`nrfutil`](https://www.nordicsemi.com/Products/Development-tools/nRF-Util) tool.

  2.1  Install the `device` command in the `nrfutil` tool:

```bash
nrfutil install device
```

3. Connect debugger to the SWD interface of the board and power ON the board

4. Program the firmware

  4.1. For Application Board 3.1, run

```bash
nrfutil device program --family nrf52 --firmware application_board_v3_rev1_fw.hex
```

  4.2. For Application Board 3.0, run:

```bash
nrfutil device program --firmware application_board_v3_rev0_fw.hex
```

5. Write the bootloader address to the (`UICR.BOOTLOADERADDR`, `0x10001014` in the reference manual: `UICR.NRFFW[0]`):

```bash
nrfutil device write --address 0x10001014 --value 0x000F0000
```

6. Optional check the bootloader start address:

```bash
nrfutil device read --address 0x10001014
```