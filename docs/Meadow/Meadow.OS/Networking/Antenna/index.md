---
layout: Meadow
title: WiFi/Bluetooth Antenna
subtitle: Understanding and switching between the onboard and external antenna options.
---

Both the Meadow F7 Feather development board and Core-Compute Module have an onboard ceramic chip antenna and a U.FL connector for an external antenna for the 2.4GHz WiFi and Bluetooth radio. Additionally, there is a software antenna switch for toggling between the two antenna; by default, the chip antenna is selected, and you must use the Meadow.OS device API to switch to the external antenna.

## Determining the Currently Selected Antenna

The current antenna in use is available via the device WiFi adapter's `CurrentAntenna` property. For example, the following code will write which antenna is currently in use to the log output:

```csharp
var wifi = Device.NetworkAdapters.Primary<IWiFiNetworkAdapter>();
Resolver.Log.Info($"Current antenna in use: {wifi.CurrentAntenna}");
```

## Switching the Antenna

Likewise, switching the antenna is also available via the device. Use a WiFi adapter's `SetAntenna()` method to change the current antenna:

```csharp
var wifi = Device.NetworkAdapters.Primary<IWiFiNetworkAdapter>();
...
wifi.SetAntenna(AntennaType.External, persist: false);
```

## Antenna Sample

For a more comprehensive example of using and changing the antenna, check out our [Antenna Switching sample](https://github.com/WildernessLabs/Meadow.Samples/blob/main/Source/Meadow%20F7/Network/AntennaSwitching/MeadowApp.cs).
