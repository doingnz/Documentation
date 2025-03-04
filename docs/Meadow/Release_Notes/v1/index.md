---
layout: Meadow
sidebar_label: Meadow v1.*
title: Meadow v1.* Releases
subtitle: Release Notes
---

## Updating Instructions

* [Meadow.CLI](/Meadow/Meadow_Tools/Meadow_CLI/)
* [Meadow.OS](/Meadow/Getting_Started/Deploying_Meadow%2EOS/)

## v1.15.0.0

This release delivers some key optimizations to Meadow networking and sleep and includes the first release of [TensorFlowLite for Microcontrollers](https://developer.wildernesslabs.co/Meadow/Meadow.Foundation/Libraries_and_Frameworks/TensorFlowLite/) support on the Meadow F7!

### Meadow.OS

* Fixed a critical issue that was affecting the reliability of Meadow Sleep/Wake
* Added support for the Quectel EG21 modem
* Minor improvements to edge-case network reliability

### Meadow.Core

* OtA download progress reporting fix
* Improved reporting of deadlock conditions
* Improved network compatibility

### Meadow.Foundation

* Added [TensorFlowLite for Microcontrollers](https://developer.wildernesslabs.co/Meadow/Meadow.Foundation/Libraries_and_Frameworks/TensorFlowLite/) support for Meadow F7
* Renamed PCanBasic assembly to prevent OEM assembly name conflict
* Added ADS1263 Driver
* Added ChromaTek WS2812 momentary and latching button drivers
* Improved WS2812 driver


## v1.14.0.0

This release delivers a major memory management upgrade that's the result of months of work. This new version of Meadow OS both reduces the total memory used and more efficiently manages freed memory.

### Updating to v1.14.0

This is a full stack release requiring an OS update and new nuget packages.

### Meadow.OS

* Greatly optimized memory usage for apps, mitigating out-of-memory issues
* Enhanced network event handling for cellular connections

### Meadow.Core

* Improvements to Linux GPIOD interop
* Added interfaces for CAN errors

### Meadow.Foundation 

* Added error support to `MCP2515`
* Added error events to PCAN device

## v1.13.0.0

This is a managed stack only release that brings a highly requested feature - CAN Bus support! 

You'll also see new peripheral drivers along with interface and abstraction improvements across the driver surface that continues to streamline and standardize the API surface.

### Meadow.Core

* Added `IDigitalPushButtonJoystick` interface 
* Added `IBacklitDisplay` interface
* Added `IColorSensor` interface
* Added `IColorInvertableDisplay` interface
* Add ability to set clock in Meadow.Linux
* Added NTP client support to Meadow.Linux
* Add implementation support for BeagleBone Black
* Meadow.Linux can now create I2C bus by bus number
* Bug fix for GPIOD interrupts
* Improvements to cellular network events

### Meadow.Foundation

* Added CAN Bus support
* New Voltaic v10x driver
* Added `Tcs3472x` color sensor driver
* Added `Ili9225` TFT SPI display driver
* Added histogram control to MicroLayout
* Added MicroGraphics APIs to invert colors on supported devices
* `Tls2591` driver cleanup and fixes
* `Xpt2046` driver cleanup and fixes
* `Mcp2515` driver cleanup and fixes
* Fixed `Pca9685` duty cycle calculation for PWM

## v1.12.8.0

### Meadow.OS

* This is a managed stack release only. No OS changes.

### Meadow.Core
  
* Added WiFi scanning support to Meadow.Linux
* Bug fixes to I2C reads in Meadow.Linux
* Improved app crash logging
* Bug fixes in F7 PWMs
* Added new `IApp<THardware>` pattern for platforms like ProjectLab
* Bug fix in app.config parser
* Bug fixes in MicroLayout (positioning inside a parent)
* Bug fix in SpiComms ReadRegister
* Bug fixes in Gnss parsing
* Improved network adapter events for wired, cell, and wifi
* Added NTP support to Cell adapter

#### Breaking changes

* PWMs now use Units for Duration and Frequency instead of the ambiguous float
* Renamed [Ft232h](https://www.nuget.org/packages/Meadow.Foundation.ICs.IOExpanders.Ft232h/) nuget package to [Ftxxxx](https://www.nuget.org/packages/Meadow.Foundation.ICs.IOExpanders.Ftxxxx)

### Meadow.Foundation
  
* Added `JsonPropertyName` to `MicroJson`
* Added support for `TimeSpan`, nullables and `List<string>` to `MicroJson`
* Added `ResistiveTankLevelSender`

#### Breaking changes

* [Servos](https://www.nuget.org/packages/Meadow.Foundation.Servos) have been refactored, fixed and improved. The previous Servo API was both confusing and likely not working. 

## v1.12.2

### Meadow.OS

* A critical memory leak affecting Meadow.Cloud authentication has been resolved.
* Support for Internet Ping & the ICMP protocol via the `System.Net.NetworkInformation.Ping` class has been added.

### Meadow.Core
  
* Improved error detection, capture and logging
* `MeadowCloudConnection` service memory and stability improvements
* Added `ReliabilityService`
* Added Raspberry Pi access to `SPI1`
* Bug fixes for Raspberry Pi serial port access

### Meadow.Foundation
  
* Added TimeSpan support to `MicroJson`
* Added ability to instantiate an Image using an `IPixelBuffer`
* Added ability to invert TFT SPI displays
* Fixed partial show on TFT SPI displays when using 12bpp color mode
* Fixed port state when initializing digital output ports for `Mcp23xxx`

#### Breaking changes

* ProjectLab no longer exposes an I2C bus or SPI directly - use connector objects to access the correct bus for the specific physical connection.

### Tooling

#### Meadow.CLI v2

* Fixed a flashing bug when specifying the OS binary file directly
* Minor output formatting fixes

#### Meadow Project Templates

* We added a new Meadow Template called StartKit, and it’s a multiplatform project Solution consisting of a Core project where you can write all the common code like business logic, main controllers, Meadow.Cloud integration, etc. referenced to a set of platform specific head projects such as `Meadow.Desktop`, `Meadow.Linux` (Raspberry Pi) and Meadow F7 devices.

Update your Meadow Templates with the command:

```console
dotnet new install WildernessLabs.Meadow.Template
```

## v1.12.0

### Meadow.OS

* Comprehensive improvements to the Meadow’s error reporting and catastrophic error recovery logic
* A WiFi access point scanning memory leak has been resolved.
* Connections to SNI-enabled TLS server endpoints are now supported
* Several minor improvements and bug fixes

### Meadow.Core
  
* Significant reliability improvements in networking stack
* General fixes and improvements in Meadow Cloud connections and reporting
* Added `IRealTimeClock`, `IBatteryBackedPeripheral` interfaces
* Added `MeadowSystemErrorInfo` class
* Added `NetworkAdapter.NetworkConnectFailed` event
* Added `MeadowCloudService.QueueCount` property
* ESP32 errors now surfaced through `MeadowSystemErrorInfo`
* Added implementation of `IWifiNetworAdapter` to Windows platform
* Bug fix in timeout-parameter device `Sleep` call
* Bug fix for invalid F7-platform CPU temp reporting

  #### Breaking changes

* `NetworkAdapter.ConnectToDefaultnetwork` is now async and returns a Task

### Meadow.Foundation
  
* Added `ADT7410` high resolution temperature sensor driver
* Added `ADXL343` accelerometer driver
* Added `PCF8523` real time clock driver
* Added `AHT10` and `AHT20` temperature and humidity sensor drivers
* Added additional escape character validation to `MicroJson`
* Added ability to fill paths in `MicroGraphics`
* Added nearest neighbor and bilinear resizing for `MicroGraphics` buffers
* Added basic rotation for `MicroGraphics` buffers
* Added ability to draw anti-aliased lines in `MicroGraphics`
* Added Rgb666 18bpp `MicroGraphics` buffer
* Added 18bpp color modes for the `ILI3941` and `ST7789` TFT SPI displays 
* Added `SimulatedLightSensor`
* General bug fixes and optimizations

  #### Breaking changes

* `PixelBufferBase.RotateAndCovert` renamed to Rotate
* `PixelBufferBase.ConvertPixelBuffer` renamed to Convert

### Tooling

#### Meadow.CLI v2

* Improved folder support for file copying and deletes
* Streamlined output when writing firmware on Mac and Linux
* Better serial port detection on Mac
* Fixed file write progress output bug
* Better OS validation when trimming and running Meadow apps
* Fixed false error when only writing runtime
* Improved debugging support
* Made build configuration check case-insentive
* Lots of general bug fixes and stability improvements

## v1.11.0.0

### Meadow.OS

  * Bugfix in WiFi implementation of POSIX `poll()` function should result in increased network stability, and increased performance for `static HttpClient`
  * Resolved crashing issue when using the “read-ahead data” `Socket.Available` property
  * Better error reporting for Cell networking connections and the TLS/HTTPS layer

### Meadow.Core
  
  * Added `OnBootFromCrash` virtual method to `App`
  * Added `IsEnabled` property to `MeadowCloudConnectionService`
  * All `Desktop` platform Displays are now `SilkDisplay` and implement `IResizablePixelDisplay`

  #### Breaking changes

  * Desktop-based applications need to remove GTK/WinForms startup and replace with `SilkDisplay.Run()`

### Meadow.Foundation
  
  * Added [`SilkDisplay`](https://www.nuget.org/packages/Meadow.Foundation.Displays.Silk) driver
  * Bug fix for [`Bmx280`](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Atmospheric.Bmx280) driver
  * Added `SimulatedAccelerometer`, `SimulatedCurrentSensor`, and `SimulatedAnalogInputPort` drivers included in our [Meadow.Foundation](https://www.nuget.org/packages/Meadow.Foundation) package

### Tooling

#### Meadow Project Templates

Update your project templates with `dotnet new install WildernessLabs.Meadow.Template` command. It includes:
  
  * All templates now use C# 10
  * Meadow.Desktop template now uses new [Silk.NET](https://dotnet.github.io/Silk.NET/)
  * Minor cleanup on the Project Lab template

## v1.10.2

This is a managed (NuGet packages) only release that improves Meadow.Cloud stability and with some minor performance improvements.

### Meadow.Core

  * Added ephemeral store-and-forwarding to Meadow.Cloud logs and events
  * Stability and user message improvements across the Meadow.Cloud stack (health reported, connection service, event publishing, etc)
  * `Meadow.Linux` added disk usage stats
  * `Meadow.Linux` added debounce support to `InterruptPort`
  * Added contracts for `IPowerSensor`, `ICurrentSensor` and `IVoltageSensor`

### Meadow.Foundation
  
  * Big update to `SC16IS752` IO expanded - thank you [kaarew](https://github.com/kaarew)!
  * [`MicroLayout`](https://developer.wildernesslabs.co/Meadow/Meadow.Foundation/Libraries_and_Frameworks/MicroLayout/) improvements including `VerticalBarChart` and `GradientBox` controls
  * Added 16x24 pixel font to [`MicroGraphics`](https://developer.wildernesslabs.co/Meadow/Meadow.Foundation/Libraries_and_Frameworks/MicroGraphics/) for high res displays
  * Added extended characters to 8x12 and 12x16 fonts
  * [`MicroJson`](https://www.nuget.org/packages/Meadow.Foundation.Serialization.MicroJson#readme-body-tab) compatibility and validation improvements
  * Bug fix for `AnalogArray` to support Core Compute modules
  * [`INA2xx`](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Power.Ina2xx) driver updates to support new sensor interfaces

#### Breaking changes

  * `Color` struct now uses float instead of double for a minor performance improvement
  * `Bmi270` namespace changed from `Meadow.Foundation.Sensors.Accelerometers` to `Meadow.Foundation.Sensors.Motion`
  * `AsciiConsoleDisplay` renamed to `AsciiConsole`

## v1.10.0

### Meadow.OS
  
  * Improvements to cell networking usability - clearer documentation and error messages
  * Improve TLS client certificate authentication

### Meadow.Core
  
  * Resolver now contains an `IJsonSerializer` - by default it is `MicroJson` but can be replaced at runtime
  * Cloud, Command/Update services have been refactored and improved
    * Connectivity is more granular (commands don’t rely on update)
    * Serialization use `MicroJson` by default
  * Linux platforms now support Meadow.Cloud authentication
  * Unhandled app crashes now send crash reports to Meadow.Cloud when enabled
  * Added on-board ACT LED to Raspberry Pi pinout

#### Breaking Changes

  * `IUpdateService` events renamed:
    * `OnStateChanged` => `StateChanged`
    * `OnUpdateProgress` => `RetrieveProgress`
    * `OnUpdateAvailable` => `UpdateAvailable`
    * `OnUpdateRetrieved` => `UpdateRetrieved`
  * New `ConnectionStateChanged` event that's triggered with Meadow.Cloud changes. You can get this event via `Resolver.MeadowCloudService`.
  * `UpdateState` enum was split in 2 enums to distinguish states between Meadow.Cloud operations (`CloudConnectionState`) and OTA Updates (`UpdateState`):
    * `UpdateState` => { `Dead`, `Disconnected`, `Connected`, `DownloadingFile`, `UpdateInProgress` }
    * `CloudConnectionState` => { `Unknown`, `Disconnected`,  `Authenticating`, `Connecting`, `Subscribing`, `Connected`, `Paused` }
  * We updated the Meadow.Cloud configuration settings:
    ```yaml
    # Meadow.Cloud configuration.
    MeadowCloud:

        # Enable Logging, Events, Command + Control
        Enabled: true

        # Enable Over-the-air Updates
        EnableUpdates: true

        # Enable Health Metrics
        EnableHealthMetrics: true

        # How often to send metrics to Meadow.Cloud
        HealthMetricsIntervalMinutes: 15
    ```
  * We made some changes to cell.config.yaml to make it more user friendly:
    * Interface field now requires: `COM1`, `COM4` and `COM6` instead of `/dev/ttyS0`, `/dev/ttyS1` and `/dev/ttyS3`
    * `TurnOnPin` was renamed to `EnablePin`
    * Now we should use MCU pin names in the `EnablePin`, to keep the consistency between that and the `ReservedPins` config
    * Adjusted some default cell settings as most users use cellular with Project Lab instead of F7 Feather:
      * Default Interface now will be `COM1`, instead of `COM4`
      * Default EnablePin will be `A3`
    * The `Csq` property and the `GetSignalStrength()` now retrieve the signal quality in `dBm`


### Meadow.Foundation
  
  * Added `Xpt2046` touch screen [driver](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Hid.Xpt2046).
  * Added `Scd30` environmental sensor [driver](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Environmental.Scd30) (thank you @RoccoDevs!)
  * Added `Ina219`, `Ina228` and `Ina260` and `Ina228` current, voltage, power monitor [drivers](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Power.Ina2xx) (thank you @engunneer!)
  * Added `Bmp280` atmospheric sensor [driver](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Atmospheric.Bmx280)
  * Added `Pca8574a` and `Pcf8574` IO expander [drivers](https://www.nuget.org/packages/Meadow.Foundation.ICs.IOExpanders.Pcx857x)
  * Added `MicroJson` - a new lightweight, IoT optimized Json serialization [library](https://www.nuget.org/packages/Meadow.Foundation.Serialization.MicroJson)
  * Updated `TextDisplayMenu` to use `MicroJson` resulting in a 75% reduction in json menu load times
  * Plus general improvements and optimizations across Meadow.Foundation

### Meadow.Tooling
  
  #### Meadow.CLI v2
  * `device provision` now supports `--gen-command`, `-id`, and `-k` parameters
  * `device info` now supports `-k`
  * `config route` now supports `local` endpoint
  * Dozens of stability and quality-of-life improvements

### Meadow.Cloud
  
  * Improved OS support for OtA updates
  * Improved subscription downgrade experience

## v1.9.0

This is a huge update for Meadow! Highlights include:

 * **Overall Stability** - With the last few releases we've knocked out nearly ever OS and networking priority-zero issue. In many cases, Meadow.OS should now be stable for weeks or months without issue.
 * **OS Multitasking Stability** - We've implemented the `Round-Robin` thread scheduler which brings a massive upgrade to how the OS manages and switches between threads and brings a new level of stability around `Thread` and `Task` operations.
 * **SPI DMA** -  We’ve added SPI DMA which reduces CPU load when communicating with SPI devices and can lead to a 30% increase in drawing performance with SPI displays!
 * **Unified Meadow.Desktop** - Meadow.Desktop got a massive simplification by unifying the launcher between Windows/macOS/Linux, meaning you now only need a single application that will run in any dekstop context for full graphics simulation.
 * **Meadow.CLI v2** - THe Meadow.CLI got a huge upgrade in its codebase with a complete re-write focused on stability, consistency, and ease-of-use.
 
**Note** - starting with v1.9.0.0 and CLI v2.0, you’ll need to [create a free Wilderness Labs account](https://identity.wildernesslabs.co/signin/register) to download new versions of the Meadow OS.

### Meadow.OS

* **Round-Robin** - .NET threads are now using the round-robin OS scheduler. This brings a much more advanced task scheduling paradigm to embedded and that better matches traditional .NET execution behavior and resolve issues of apps “livelocking” because of a tight loop preventing progress under the First-In, First-Out (FIFO) scheduler.
* **SPI DMA** - SPI DMA has been enabled for all SPI data transfers. Use of it should be transparent, providing approximately 3x throughput speed for SPI peripheral devices.
* **Coprocessor Threading Stability** - Changes to the threading on the coprocessor were made, resulting in greater stability for network requests
* **Deep OS Internal Stability Fixes** - Several low-level fixes & improvements that provide more stability throughout the entire OS stack.

### Meadow.Core

* Support has been added for F7 multi-platform targeting.  One app assembly can now contain IApp instances for multiple F7 hardware targets. (add link to docs).
* `IPixelDisplayProvider` interface added for Meadow.Desktop platforms.
* SensorService now auto-registers any `ISleepAwarePeripherals` it knows about.
* Improvements to Core interrupt handling in F7 platforms.
* Interrupts events changed from containing a DateTime to a system tick (for performance reasons).
* OtA Downloads now report progress via an event.
* Added “reason” to network disconnection events on F7 platforms.
* Added preliminary support for Raspberry Pi 5.

### Meadow.Foundation

* FT232H/FTDI Driver refactored to support multiple devices at one time and to use the same driver (FT2xxx) for all modes.
* Improved partial update logic in MicroGraphics and TftSpi display drivers.
* BME688 gas resistance fix. Thanks to community member `Laszlo` for the fix.
* SCD40 events fix.

#### Breaking changes

* Renamed `IGraphicsDisplay` to `IPixelDisplay` and moved to `Meadow.Contracts` and changed namespace to `Meadow.Displays `.
* Moved `IPixelBuffer` to `Meadow.Contracts` and namespace changed to `Meadow.Displays`.

### Meadow.Cloud

* Bug fix for Azure Event Grid data serialization
* For over-the-air updates, we exposed a new event, `OnUpdateProgress` that is triggered periodically showing the update’s download progress expressed in bytes.

### Meadow.Desktop

* We have added support for `Meadow.Desktop` as a target. This allows a single app to target Windows, Mac or desktop Linux with auto-platform detection and simulated `IPixelDisplay`. New templates are coming soon to make `Meadow.Desktop` app creation simple.

### IoT Accelerators

* Our GNSS Tracker got a big update with its v2 hardware iteration (which is packed with more sensors than its predecessor), including a revamped demo application displaying accurate atmospheric sensor data along with battery and solar input voltage.

### Meadow.Tooling

* [CLI v2.0](https://developer.wildernesslabs.co/Meadow/Meadow_Tools/Meadow_CLI/) has shipped! This is a massive rework of the command line tool used to communicate with Meadow devices and manage firmware. Note, with this new release, you will need to [create a free Wilderness Labs account](https://identity.wildernesslabs.co/signin/register) and sign in before downloading firmware updates.

## v1.8.0

### Meadow.OS & Meadow.Core

* Resolved instability issues when using multiple TLS connections simultaneously, closing issues [#355](https://github.com/WildernessLabs/Meadow_Issues/issues/355) and [#380](https://github.com/WildernessLabs/Meadow_Issues/issues/380)
* Meadow.Units added static `Zero` properties to `Angle`, `Power`, `Resistance`, and `Voltage`
* Meadow.Units added construction extensions to `Frequency`, `Resistance`, `Length` and `Temperature`

### Meadow.Foundation

### New Drivers

* New [Useful Sensor’s Tiny Code Reader QR](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Cameras.UsefulSensors.TinyCodeReader) code scanner driver
* Added methods to to draw vertical and horizontal gradients to `MicroGraphics`
* Added method to draw buffers with a transparency (ignore) color
* Event cleanup on environmental drivers

## v1.7.0

### Meadow.OS & Meadow.Core

* `System.Debug.WriteLine` is now functional and no longer crashes the device
* New property added to Meadow.Core NetworkAdapters: `DnsAddresses`
* Added SensorService, read more [here](https://blog.wildernesslabs.co/using-meadows-sensorservice-to-optimize-sensor-reads-into-a-single-thread/).
* Several low-level fixes & improvements

### Meadow.Foundation

#### New Drivers

* New [OLED 128x64 Featherwing](https://www.nuget.org/packages/Meadow.Foundation.FeatherWings.OLED128x64Wing)
* New Useful Sensor’s [`PersonSensor`](https://www.nuget.org/packages/Meadow.Foundation.Sensors.PersonSensor)
* New Infrared camera [`Amg8833`](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Camera.Amg8833)
* New [`AsciiConsole` display](https://www.nuget.org/packages/Meadow.Foundation.Displays.AsciiConsole)
* New [`DFRobot Gravity Dissolved Oxygen` sensor](https://www.nuget.org/packages/Meadow.Foundation.Sensors.Environmental.DFRobotGravityDOMeter) driver
* Mac keyboard support added to keyboard driver
* `SH1107` display driver cleanup and fixes
* Improved relay API and contracts
* General cleanup of sensor contracts 
* General cleanup and memory optimizations

### Breaking changes

* Moved `Color` struct to `Meadow.Contracts` and changed namespace to `Meadow`
* MicroLayout - Property `Visible` on all controls has been renamed to `IsVisible`
* MicroLayout - Property `Filled` on Box has been renamed to `IsFilled`

### Meadow.Cloud

* Added new integration for Azure Event Grid

## v1.6.0

### Meadow.OS

* Resolved a memory leak that occurs in common network operations over Wifi. Improves device reliability when using WiFi.
* Various minor fixes and improvements

### Meadow.Core

* Added support for high-speed ADC calls for F7 platform
* Added several interfaces for motors: `IMotor`, `IVariableSpeedMotor`, `IPositionalMotor` and `IStepperMotor`
* Added `IDissolvedOxygenSensor` interface
* Added SensorService
* Refactor and clean-up of `Updated` event for `ISamplingSensor<T>` implementations

### Meadow.Foundation

#### New Drivers

* `StepDirMotor` and CwCcwMotor stepper motors
* Atlas Scientific Gravity Dissolved Oxygen sensor

#### Fixes/Updates

* New composite driver pattern improves authoring drivers that implement multiple sensor contracts
* Improved behavior of serial distance sensor drivers for single reads and sampling

## v1.5.0

### Meadow.OS

* Fixed an issue where the TLS subsystem (mbedTLS) was racing on initialization, generating intermittent issues with connecting to HTTPS endpoints
* Upgraded external flash driver. This resolves issues with intermittent hanging after a software reset, which affected Meadow error recovery

### Meadow.Core

* Added Meadow.Core API support for disabling server certificate validation for TLS (HTTPS) connections using MeadowOS.SetServerCertificateValidationMode()
* Clean up and performance improvements in F7 serial ports.
* Added F7 os-level protection around mq operations
* IPin extensions moved up in namespace to improve discoverability
* Added SerialMessagePort convenience methods to appropriate Connectors

### Meadow.Foundation

#### New Drivers

* A02YYUW serial distance sensor

#### New Features

* Added IDisposable to all appropriate drivers

#### Fixes/Improvements

* MicroLayout chart layout improvements
* MicroGraphics fix exception when calling DrawImage
* Add sensor interfaces to BMI270
* Improved null reference checking
* WinForms Display Screen updated and improved, now a movable window showing on the center of the screen when running, and buffer boundaries fixed.

### Meadow.Cloud
* Users can now create, edit, and manage API Keys to access search and command endpoints.

### Meadow.CLI

#### V1 1.5.0
  * Improve dependency filter for App.dll
  * Do a directory existing check before we check for the internet connection

#### V2 Alpha.4
  * Trimming Enabled
  * Fixed an issue where if device.Runtime didn’t have a corresponding local directory, it would break `meadow app deploy`


## v1.4.0

### Meadow.OS
* Fixed stability issues when using more than 4 connections on WiFi (https://github.com/WildernessLabs/Meadow_Issues/issues/347)
* Fixed a minor issue with processing a malformed `wifi.config.yaml`
* The default gateway is now added to the list of DNS servers on WiFi

### Meadow.Core

* Added `IRheostat` and `IPotentiometer` interfaces
* Bug fix for Meadow.Windows `GetPortNames`
* GPIOs are initialized to inputs with no resistor on Core initialization

### Meadow.Units

* New digital storage unit
* New Apparent Power unit
* New Reactive Energy unit
* New Reactive Power unit
* Cleanup and typo fixes 

### Meadow.Foundation

#### New Drivers

* Mcp4xxx Potentiometers and Rheostats
* Grove 4-Channel SPDT Relay
* mikroBUS SPI 4-20mA receiver click boards

#### New Features

* Added library to support M-Bus (Meter Bus)
* Project Lab now lazy-loads sensor drivers

#### Fixes/Improvements

* MicroLayout `DisplayScreen` refresh bug fix
* MicroGraphics improved circle drawing accuracy
* New `Blend` extension method for `Color`
* Improved nullable checks and null validation
* A lot of cleanup - thanks Engunneer!

### Meadow.Cloud

Public Beta Launch: https://www.meadowcloud.co/

### Meadow.CLI

* V2 Alpha.1
  * Allow sequential flashing of devices in bootloader mode. 
  * `--verbose` should now work across commands.
  * Duplicate logging removed from `meadow listen`
  * Color-coded logging (more to come)

## v1.3.4

### Meadow.OS
* Fixed issue with Azure IoT hub certificates.
* Fixed issue where invalid credentials in wifi.config.yaml could lock the board.
* Changed the way the system checks for the minimum required file set.

### Meadow.Core
* Bug fix for finding app settings file in Meadow.Linux and Meadow.Windows
* Added `GetMemoryAllocationInfo` and `ProcessorLoad` for F7 `PlatformOS`
* Interface break: Refactor `ISerialPort` `ReadAll` method
* Added interfaces and enums for cellular states and data

### Meadow.Foundation

#### New Drivers
* PCx857x family of digital IO expanders
* ElectroMagnetic Relay Board
* LSM6DSOX iNEMO inertial module with Machine Learning Core
* LIS3MDL digital magnetic sensor
* HC2 atmospheric sensor
* BG95-M3 GNSS driver
* 9-DOF IMU Featherwing

#### New Features
* Added support for Modbus RTU server
* Updated MicroLayout class names [Interface break]
* Added `LineChart` to MicroLayout
* `SpiCommunications` now explicitly asserts the CS line on startup
* x74595 support parallel writes
* x74595 asserts chip select state at startup
* MicroGraphics Image class supports BI_BITFIELDS compression for 24bpp images

#### Fixes
* Renamed `BidirectionalDcMotor` `Clockwise` and `CounterClockwise` methods [Interface break]
* `WinForms` display driver `WriteBuffer` fixed
* GNSS drivers updated to conform to `IGnssSensor` interface
* BME688 gas resistance output fixed
* `TextDisplayMenu` `OnOff` item fixed
* `TextDisplayMenu` item type now returned on change events
* LIS2MDL output scaling fixed
* A lot of cleanup, spelling fixes, XML comment additions, etc.

More information here: [v1.3.4 Milestone](https://github.com/WildernessLabs/Meadow.Foundation/milestone/29)

### Meadow.Cloud
*  Overhaul of log viewer and a number of other UI improvements

### Meadow.CLI
* Update dfu-util version check to check for v0.11
* Only push App.dll to the device Fixes Issue 340

### VS Extensions
* Bump to 1.3.4 to include the aforementioned Meadow.CLI changes.

## v1.3

### Meadow.OS
* Added limited TLS client certificate support
* Reliability improvements for OS OTA updates
* Stability and usability improvements for cell networking:
  * `NetworkConnected`/`NetworkDisconnected` events added to `CellNetworkInterface`
  * Support for scanning cell networks added via `F7CellNetworkAdapter.Scan()`
  * Exposed module IMEI and cell signal strength properties via `F7CellNetworkAdapter.Imei` and `.Csq` properties
  * Greatly improved network reconnect speed when connection is dropped
  * Fixed an issue with BG95 not turning when resetting Meadow
  * IPCP-provided DNS servers are now prioritized for use by default

### Meadow.Core
* Easily add health metrics reporting to Meadow.Cloud. To enable this, add the following to  `app.config.yaml`:  

```yaml
HealthMetrics:
  Enabled: true
  Interval: 10
```

(Interval is in minutes.) Health metrics get sent to Meadow.Cloud once a network connection is available.

### Meadow.Foundation
* Sc16is7x2 - new UART expander driver
* NeoPixel Featherwing - new driver
* My7000s - improved sampling logic
* MaxBotix - improved sampling logic for serial sensors
* MicroLayout - adding `ScaleFactor` to `DisplayLabel`
* MicroGraphics - fixed negative Y out of bounds exception
* MicroGraphics - fixed index bug for 12x16 font
* SwitchingRainGauge - sample updated to to avoid D15 error
* Updated all projects to C## 10

### Meadow.Cloud
* Receive health metrics from device and update `LastHeartbeat` and `Version` in the device list
* Retrieve log and event data via Webhook and Azure Event Hubs integrations

### Meadow.CLI
* New Classic build for some customers having issues on Windows 10 and some Windows 11 machines. Please download from [here](https://github.com/WildernessLabs/Meadow.CLI/releases/tag/v1.3.0.0). 
* If the runtime version is unknown (typically on brand new boards), it will force a flash erase, without prompting.
* Simplified meadow packaging with a project target (instead of folder/file) that builds and trims assemblies before creating an MPAK.

### VS Extensions
* VSCode
  * Support for Microsoft's new 2.x C## Extension
  * Due to dropping OmniSharp support extensions should now load a bit quicker.
  * Attached devices now appear in the configuration list.
  * Ability to toggle between Debug and Release configurations before deploying to your Meadow.

### Known Issues
* Device Sleep/Wake is known to have intermittent stability issues that we are investigating.

## v1.2

### Meadow.OS
* Greatly improved reliability of cell networking
* Extended maximum low-power mode sleep time from 18 hours to 25 days
* Enhanced Ethernet driver & added support for ethernet connect after startup
* Adjusted thread priorities aiming to improve responsiveness in debugging

### Meadow.Core
* Greatly improved app startup time
* Improved latency of first interrupt
* Added app-accessible Settings to `IApp`
* Added `StateChanged` event to `IUpdateService`
* Bug fix in refreshing network adapter info
* Added support for Connectors
* Bug fix for incorrect scaling in `AnalogInputPort`
* Integrated cell networking support via the new `CellNetworkAdapter` class
* Added a Cloud Log Provider to send logs and events to Meadow.Cloud

### Meadow.Foundation
* New MicroLayout library - a lightweight UI framework that works with MikroGraphics
* New ME007YS ultrasonic distance sensor driver
* Fixed ST7789 display support for 320x240 displays
* Fixed GC9A01 display reset bug
* Bug fix in MicroGraphics vertical alignment

### Meadow.Cloud
* View device logs and events. The following filters are applicable in the search box: `source:log|event` `deviceId:{deviceId}`
* Added a Metadata field to the package publish flow to pass metadata to the Update Service.  [Issue 319](https://github.com/WildernessLabs/Meadow_Issues/issues/319)
* Updated the MQTT service infrastructure. Meadow.Core update required for OtA compatibility.

### Meadow.CLI
* Added a new parameter for `--metadata` during `package publish`. This metadata is passed through to the Update Service and can be used to determine which devices to update. [Issue 319](https://github.com/WildernessLabs/Meadow_Issues/issues/319)
* `package create` fix for incorrect Windows backslash: [Issue 300](https://github.com/WildernessLabs/Meadow.CLI/pull/300)

### VS Extensions
* [VS2022-Windows] The Meadow tab should now receive focus after deployment.
* [VS2022-Windows] The Meadow tab’s logs should be cleared each debugging run.
* Due to the debugging priority change in the OS, debugging should be more responsive in all the extensions.

## v1.1

### Meadow.OS
* Added support for the BG95 (LTE-M) and M95 (GSM) cellular modules, [view documentation](http://developer.wildernesslabs.co/Meadow/Meadow.OS/Cellular/).
* Improved reliability of cell networking
* Resolved issue where using a static IP address and Wi-fi auto-connect together would not work as expected

### Meadow.Core
* Added Meadow.LogProviders library, which includes Console, File and UDP logging
* Bug fix in F7 internal resistors (resistors inverted)

### Meadow.Foundation
* New driver: NeoPixel driver
* New driver: Mcp3xxx family of analog to digital converters
* New driver: Current Transducer
* New driver: microBUS AC Current current sensor driver
* New driver: microBUS LEM current sensor driver
* New driver: Pca9671 IO expander driver
* Minor fixes and enhancements - [details here: v1.1.0 Milestone (github.com)](https://github.com/WildernessLabs/Meadow.Foundation/milestone/26)

### Meadow.Cloud
* Multi-org support and ability to invite users

### Meadow.CLI
* Added support for `app.build.yaml` to allow NoLink per-assembly
* Fix for `meadow list ports` command on Linux and therefore VSCode

## v1.0.2

### Meadow.OS
* Minor OtA enhancements

### Meadow.Core
* `ISerialPort` now follows the Meadow controller pattern
* Minor improvements to interrupt handling
* `UpdateService` catches exceptions while unzipping MPAKs and raises an event

### Meadow.Foundation
* `TftSpi` - Fixed rotation bug for the ST7789 display

### Meadow.Cloud
* Ability to manage collections and publish to specific collections

### Meadow.CLI
* Meadow.Cloud compatibility changes for creating packages and listing collections

### Meadow.Linux
* Added support for processor temperature

## v1.0 

The culmination of six years of work and 1.5MM lines of code, the Meadow v1.0 release includes all of the features found in the previous RC-3.1 release and adds final touches for OtA updates reliability and security.

For more information about recent work on Meadow.OS, please have a look at our [Release Candidate Release Notes](/Meadow/Release_Notes/Release-Candidates/).

### Updating to v1.0

This is a full stack release requiring an OS update, new nuget packages, a new Meadow CLI and new Visual Studio extensions.

### Updating Meadow.CLI

Start by making sure you have the latest version of the CLI (1.0.0) by running:

```bash
dotnet tool update Wildernesslabs.Meadow.CLI --global
```

### Updating Meadow.OS

Download the latest version of Meadow.OS:

```bash
meadow download os
```

Update by putting your Meadow device in boot loader mode and running:

```bash
meadow flash os
```