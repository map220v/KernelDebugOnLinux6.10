# USB(DWC3) Kernel Debug On Linux 6.10

Based on: https://github.com/jacktang310/KernelDebugOnNexus6P

Instruction:
1. Enable CONFIG_KGDB, CONFIG_KGDB_SERIAL_CONSOLE, CONFIG_USB_G_SERIAL and Disable CONFIG_QCOM_WDT(or any other watchdog your device has) in kernel config.
2. Add to kernel cmdline ```kgdboc=ttyGS0``` or after booting target device run ```echo ttyGS0 > /sys/module/kgdboc/parameters/kgdboc```
3. Run ```echo g > /proc/sysrq-trigger``` on target device.
4. Attach gdb. ```sudo gdb-multiarch vmlinux -ex "target remote /dev/ttyACM0"```

KGDB should fully work until usb cable disconnected.
Manual KGDB break using sysrq-trigger should be possible until mass crash of DSP's, WiFi, IPA and other subsystems, caused by "paused interrupts" while debugging.