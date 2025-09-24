[Click here](../README.md) to view the README.

## Design and implementation

The design of this application is minimalistic to get started with code examples on PSOC&trade; Edge MCU devices. All PSOC&trade; Edge E84 MCU applications have a dual-CPU three-project structure to develop code for the CM33 and CM55 cores. The CM33 core has two separate projects for the secure processing environment (SPE) and non-secure processing environment (NSPE). A project folder consists of various subfolders, each denoting a specific aspect of the project. The three project folders are as follows:

**Table 1. Application projects**

Project | Description
--------|------------------------
*proj_cm33_s* | Project for CM33 secure processing environment (SPE)
*proj_cm33_ns* | Project for CM33 non-secure processing environment (NSPE)
*proj_cm55* | CM55 project

<br>

In this code example, at device reset, the secure boot process starts from the ROM boot with the secure enclave (SE) as the root of trust (RoT). From the secure enclave, the boot flow is passed on to the system CPU subsystem where the secure CM33 application starts. After all necessary secure configurations, the flow is passed on to the non-secure CM33 application. Resource initialization for this example is performed by this CM33 non-secure project. It configures the system clocks, pins, clock to peripheral connections, and other platform resources. It then enables the CM55 core using the `Cy_SysEnableCM55()` function and the CM55 core is subsequently put to DeepSleep mode.

In the CM33 non-secure application, the clocks and system resources are initialized by the BSP initialization function. The retarget-io middleware is configured to use the debug UART, and the USER LED3 is initialized.

Using the Device Configurator tool, the PWM peripheral is configured to produce a 2 Hz output with duty cycle set to 50%. The clock frequency is set to 2 kHz and the period value is set to 2000 so that the time taken for 2000 counts is 1 second and the frequency is 1 Hz. The compare value is set to 1000 so that the duty cycle is 50% which gives 2 Hz output.

In this configuration, the PWM generates a square wave which is connected to USER LED3. This LED blinks at 500 ms (inverse of the PWM output frequency, 2 Hz). After the PWM output becomes available, the CM33 CPU enters Sleep mode to conserve power.

Change the clock frequency and period value using the device configurator tool to vary the PWM frequency and change the compare value accordingly to vary the duty cycle. Save the Device Configurator, build and reprogram the application to observe the change in the LED blink pattern.

You may also route the PWM output to any GPIO pin exposed on the kit and observe the output via Logic Analyzer.

<br>