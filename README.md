# Intel BE200 6 GHz Wi‑Fi Full 6Ghz Band on Windows — Driver 23.0.6.4 / AX411 / AX210 Testing (Working)

Real-world Windows testing of **Intel BE200 320MHz Wi‑Fi 7 / 6 GHz**, with additional **Intel AX411** observations and **AX210** candidate notes. The confirmed BE200 setup uses Intel driver **23.0.6.4 / Netwtw14** and has established active 802.11be connections on representative 6 GHz channels from **37 through 213**.

Keywords: **Intel BE200 6GHz Windows, BE200 driver 23.0.6.4, Wi‑Fi 7 6GHz, AX411 6GHz, AX210 6GHz, Netwtw14, 802.11be**.

> **Important:** This is a technical test record, not a regulatory-bypass guide. Channel availability and permitted operation depend on the AP, client, firmware, driver, and local regulations. Use only frequencies/channels permitted for your location and equipment.

## Confirmed Test Platform

| Component | Test result |
|---|---|
| Motherboard | **Gigabyte B760M DS3H AX Rev. 1.2** |
| Confirmed adapter | **Intel Wi‑Fi 7 BE200 320MHz — standalone PCIe/M.2** |
| Built-in adapter | **Intel AX411 / CNVio2 — 6 GHz scan and active association now confirmed with driver 23.0.6.4; stable 2402/2402 Mbps PHY reproduced on Channel 37** |
| Operating system | Windows |
| Tested Intel driver | **23.0.6.4** |
| Working driver branch/service | **Netwtw14** |
| Windows region state used for the successful AX411 reproduction | **Country or region: United States (GeoId 244)** and **Device setup region: United States** |

## Main Result

With the standalone Intel BE200 and Intel driver **23.0.6.4 / Netwtw14**, Windows successfully detected and actively connected to 6 GHz Wi‑Fi at multiple widely separated channel positions, including the lower, middle, high and top end of the tested range.

| 6 GHz channel | Windows protocol | Driver | Windows aggregated link speed shown in test capture |
|---:|---|---|---:|
| **37** | 802.11be | 23.0.6.4 | **4803 / 4803 Mbps** |
| **53** | 802.11be | 23.0.6.4 | **4323 / 4323 Mbps** |
| **69** | 802.11be | 23.0.6.4 | **4323 / 4323 Mbps** |
| **85** | 802.11be | 23.0.6.4 | **4323 / 4323 Mbps** |
| **101** | 802.11be | 23.0.6.4 | **4323 / 4323 Mbps** |
| **133** | 802.11be | 23.0.6.4 | **5188 / 5188 Mbps** |
| **149** | 802.11be | 23.0.6.4 | **4323 / 4323 Mbps** |
| **165** | 802.11be | 23.0.6.4 | **5188 / 5188 Mbps** |
| **213** | 802.11be | 23.0.6.4 | **4803 / 4803 Mbps** |

These are active Windows connection results, not only passive scan visibility.

The BE200 currently follows the 6 GHz channel selected on the AP/router directly in the tested setup. After the setup became stable, repeated adapter disable/re-enable was **not required** for normal BE200 operation.

The BE200 link rate is dynamic. In separate testing the link has also reached approximately **5764 Mbps** under favorable conditions.

## Screenshot Evidence Already Stored in This Repository

![Intel BE200 Windows Network Properties — test screenshot 1](screenshots/1111.png)

![Intel BE200 Windows Network Properties — test screenshot 2](screenshots/22.png)

Additional active-connection screenshots have been captured for Channels **37, 133, 149, 165 and 213** and can be stored as individual image files for permanent visual evidence.

## Active Connection Proof — Channel 101

```text
SSID           : TP-Link_5G-6G_MLO / TP-Link_6G_be
Protocol       : 802.11be
Adapter        : Intel(R) Wi-Fi 7 BE200 320MHz
Driver Version : 23.0.6.4
Network Band   : 6 GHz
Channel        : 101
Link Speed     : 4323 / 4323 Mbps (published Windows Properties capture)
Security       : WPA3-Personal
```

A live `netsh wlan show interfaces` capture from the same test platform also confirmed an active 6 GHz / 802.11be connection on Channel 101.

## Active Windows UI Proof — Channels 37 / 133 / 149 / 165 / 213

```text
Channel 37  : 802.11be / 6 GHz / 4803 / 4803 Mbps
Channel 133 : 802.11be / 6 GHz / 4803 / 4803 Mbps
Channel 149 : 802.11be / 6 GHz / 4323 / 4323 Mbps
Channel 165 : 802.11be / 6 GHz / 5188 / 5188 Mbps
Channel 213 : 802.11be / 6 GHz / 4803 / 4803 Mbps
```

This is stronger evidence than scan visibility alone because Windows shows an established Wi‑Fi 7 connection on each of these channel positions.

## PowerShell / NETSH Scan Evidence

Useful commands:

```powershell
netsh wlan show interfaces
netsh wlan show networks mode=bssid
```

Previously captured scan evidence includes Channel 101 and Channel 165 as 6 GHz / 802.11be networks.

Example Channel 101 scan:

```text
SSID : TP-Link_5G-6G_MLO
    Authentication          : WPA3-Personal
    Encryption              : CCMP
    BSSID 1                 : ba:6e:84:e3:5d:f5
         Signal             : 89%
         Radio type         : 802.11be
         Band               : 6 GHz
         Channel            : 101
         Details            : (H2E Required) (MLD)
```

Example Channel 165 scan:

```text
SSID : MobSoftAP_Router
    Authentication          : WPA3-Personal
    Encryption              : CCMP
    BSSID                   : 36:63:b2:35:86:52
    Signal                  : 86%
    Radio type              : 802.11be
    Band                    : 6 GHz
    Channel                 : 165
    Details                 : (H2E Required) (MLD)
```

Channel 165 is additionally confirmed by an **active Windows connection** at **5188 / 5188 Mbps**.

## BE200 Stability Observation

During earlier testing with the old Intel driver, 6 GHz discovery could sometimes take a few minutes. A quick Wi‑Fi adapter disable/re-enable can refresh discovery in such situations. However, on the current BE200 setup the connection is now operating **without requiring repeated adapter resets or enable/disable cycles**.

```text
BE200 + 23.0.6.4 / Netwtw14
→ stable 6 GHz operation in the present setup
→ direct connection to the AP-selected tested channel
→ no repeated enable/disable workaround currently required
```

This should not be interpreted as a guarantee that every system will have identical discovery timing.

## AX411 — Newly Confirmed 6 GHz Result

The motherboard-integrated **Intel AX411 160MHz (CNVio2)** has now been directly and repeatedly validated with Intel driver **23.0.6.4**.

Confirmed observations on this system:

- Direct 6 GHz BSSIDs become visible under the successful Windows region configuration described below.
- Active 6 GHz association was reproduced on **Channel 85**, **Channel 165**, and **Channel 37**.
- On **Channel 37**, the AX411 reached its full **2402 / 2402 Mbps** Wi-Fi 6E PHY rate.
- The 2402 / 2402 Mbps result held across three consecutive samples taken 10 seconds apart.
- During that stable Channel 37 test Windows reported **93% signal / -41 dBm RSSI**.
- BE200 was disabled during the AX411 validation, so the result is independently attributable to the motherboard-integrated AX411.

Stable AX411 capture:

    Adapter      : Intel(R) Wi-Fi 6E AX411 160MHz
    Driver       : 23.0.6.4
    SSID         : MobSoftAP_Router
    Band         : 6 GHz
    Channel      : 37
    Radio type   : 802.11ax
    Receive rate : 2402 Mbps
    Transmit rate: 2402 Mbps
    Signal       : 93%
    RSSI         : -41 dBm

Repeated stability check:

    Sample 1: 6 GHz / Ch 37 / 2402 / 2402 Mbps / -41 dBm
    Sample 2: 6 GHz / Ch 37 / 2402 / 2402 Mbps / -41 dBm
    Sample 3: 6 GHz / Ch 37 / 2402 / 2402 Mbps / -41 dBm

AX411 also established an active 6 GHz connection on Channel 165, confirming that the result is not limited to the lower 6 GHz channel used for the 2402 Mbps stability test.

### Client 6 GHz vs 6 GHz P2P GO

With driver 23.0.6.4, AX411 reports:

    P2P GO on 6 GHz : Not Supported
    P2P SAE on GO   : Not Supported

This does **not** prevent normal 6 GHz client/STA operation. The live tests above confirm that 6 GHz client connectivity and 6 GHz P2P GO / hotspot capability are separate paths.

## AX210 / AX211 Candidate Notes

The **Intel AX210** is a standalone PCIe/USB M.2 Wi‑Fi 6E adapter and is therefore a stronger candidate for this experiment than CNVio2-based AX211/AX411.

Public user reports show AX210 6 GHz operation working with older Intel drivers in situations where newer drivers did not expose 6 GHz correctly. Some reports also describe delayed discovery and improvement after an adapter disable/re-enable cycle.

Those reports support AX210 as a plausible candidate, but the exact multi-channel behavior documented here with BE200 still requires direct AX210 testing on this project.

```text
AX210 (PCIe/USB M.2) → Not yet tested here; strong candidate. Older-driver 6 GHz operation reported publicly.
AX211 (CNVio2)       → Different platform-integrated architecture.
AX411 (CNVio2)       → Confirmed 6 GHz active association; stable 2402/2402 Mbps at Ch 37 with 23.0.6.4.
BE200 (PCIe/USB M.2) → Confirmed working and currently stable in this project.
```

## Windows Region / Location Settings — Reproduced A/B Result

The current AX411 tests showed that **three Windows location/region settings matter on this test system**:

1. **Country or region** = United States
2. **Device setup region** = United States
3. **Default location (map pin)** = a location in the United States

The successful Windows state used in the reproduced test included:

    Country or region   : United States
    Device setup region : United States
    Default location    : United States map location

`Get-WinHomeLocation` reported:

    GeoId 244  United States

### Default location / map pin

Windows **Default location** was also set to a U.S. location. In the reproduced setup, this setting is considered part of the working configuration.

Path:

    Settings → Privacy & security → Location → Default location → Set default

Example test location used:

    721 Beckman Ln, Texline, TX 79087, United States

This is separate from `Set-WinHomeLocation -GeoId 244`. The Home Location / GeoId and the Windows Location-service default map location are different settings.

### India vs US A/B test

With **India / GeoId 113**, after refreshing the adapter, direct selectable 6 GHz BSSID visibility disappeared in the reproduced test. 6 GHz entries could still appear only as colocated-AP metadata attached to 5 GHz MLO-capable BSSIDs.

After returning **Country or region** to **United States / GeoId 244**, while **Device setup region** and **Default location** were also set to the United States, the direct 6 GHz SSID returned and the AX411 connected again on 6 GHz.

Example successful reconnection after returning to the U.S. configuration:

    Adapter    : Intel(R) Wi-Fi 6E AX411 160MHz
    SSID       : TP-Link_6G_be
    Band       : 6 GHz
    Channel    : 165
    Radio type : 802.11ax

### Discovery delay / adapter refresh

After changing the region/location configuration, 6 GHz may not appear instantly. In this testing it can take roughly **1–2 minutes**. Disabling and re-enabling the Wi-Fi adapter/radio usually refreshes discovery faster.

Example refresh:

    Disable-NetAdapter -Name "WiFi" -Confirm:$false
    Start-Sleep -Seconds 3
    Enable-NetAdapter -Name "WiFi" -Confirm:$false

> **Important:** These are reproduced Windows test observations, not a claim that Windows Home Location, Device setup region, or Default location is universally identical to the Wi-Fi RF regulatory domain. Users must still follow the regulations applicable to their location and equipment.

## What “No Modification” Means

The successful BE200 result does **not** use:

- patched Intel `.sys` files
- custom Intel firmware
- a `DisableLAR` registry hack
- a forced `CountryCode` / `RegDomain` value
- Windows regulatory database editing
- custom Windows system files
- Linux `iw reg set`

The working package is an Intel Windows Wi‑Fi driver package, with Windows reporting **23.0.6.4 / Netwtw14**.

The working BE200 registry export was checked for obvious user-level regulatory overrides. No explicit `DisableLAR`, `CountryCode`, `RegDomain`, `RegulatoryDomain`, FCC/world-domain override, or similar country-forcing value was found.

Intel-defined 6 GHz settings in the driver package include normal parameters such as:

```text
Is6GhzBandSupported
ChannelWidth6
RoamingPreferredBandType
```

These are ordinary Intel adapter options, not evidence of a regulatory bypass.

## Driver Package / OEM Observation

The tested **23.0.6.4** package is an Intel Wi‑Fi driver distributed through a Dell/OEM package path.

Static inspection of the driver binaries shows OEM-specific strings and handling, including examples such as:

```text
Dell Inc.
Alienware
EnableDellSmartAntenna
```

This confirms that OEM-specific platform handling is compiled into the Intel driver codebase. It does **not** by itself prove that a Dell-specific runtime path is responsible for the observed 6 GHz behavior on this motherboard.

## Why the Older Intel Driver Can Behave Differently

A strings-level comparison was made between the working **Netwtw14** binary and a newer **Netwtw18/Netwaw18** branch binary.

Both contain Intel LAR/regulatory-related logic, so the working result should **not** be described as “LAR removed” or “LAR disabled.”

Importantly, the symbol:

```text
prvLarRemoveBssEntriesWithInvalidChannels
```

is present in the old branch as well as the newer branch. Therefore, the presence of this function alone does **not** explain the behavioral difference.

The newer branch exposes more explicit OEM/platform regulatory-policy machinery, including strings associated with:

```text
CnvUefiWlanUATS
UefiCnvWlanUNEB
DSM3 - WiFi 6E country settings
DSM9 - OEM disabled bands
mhiffProcessMccAllowedApTypeTable
larSendMccAllowedApTypeApi
getWifiCountryRegionList
```

The old branch also contains OEM/UHB-related capability handling, but the newer branch appears to integrate these platform/OEM inputs more explicitly into regulatory and allowed-AP-type processing.

This is static binary evidence only. It does **not** prove which exact path executes for a particular connection, and it should not be treated as instructions for disabling regulatory enforcement.

## Required / Tested Driver

```text
Intel Wi‑Fi Driver : 23.0.6.4
Driver branch      : Netwtw14
```

For the closest reproduction, use the same driver version. A **clean install is recommended**, because Windows may automatically bind a newer Intel Wi-Fi package from Windows Update or from the local Driver Store.

### Clean driver installation

1. Temporarily disconnect the PC from the Internet.
2. Open **Device Manager → Network adapters**.
3. Select the Intel Wi‑Fi adapter.
4. Choose **Uninstall device**.
5. If shown, select **Attempt to remove the driver for this device**.
6. Reboot if requested.
7. Install Intel Wi‑Fi driver **23.0.6.4**.
8. Reboot Windows.
9. Verify the active version under **Device Manager → adapter → Properties → Driver**.

If Windows keeps restoring another Intel package from the Driver Store, remove the unwanted package first. Do not let Windows Update replace the test driver while reproducing the result.

## Evidence Summary

| Evidence | Ch 37 | Ch 101 | Ch 133 | Ch 149 | Ch 165 | Ch 213 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| Seen in BE200 testing | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| 802.11be shown by Windows | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Active Windows connection proof | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Windows Properties link-speed capture | 4803 | 4323 | 4803 | 4323 | 5188 | 4803 |
| NETSH / Windows evidence documented | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

The table documents representative channel positions that were actively tested. It should not be interpreted as proof that every possible 6 GHz channel has individually been tested unless a corresponding test record is added.

## Save Your Own Evidence

```powershell
netsh wlan show networks mode=bssid > 6ghz-scan.txt
netsh wlan show interfaces
```

Useful reproduction details include motherboard/CPU, adapter model, whether the adapter is CNVio or standalone PCIe/M.2, exact Intel driver version, Windows build, Windows Home Location, AP/router model and firmware, selected 6 GHz channel, and raw `netsh` output.

## Compatibility Notes

Behavior may vary with Intel CPU/platform generation, motherboard M.2/CNVio/PCIe implementation, adapter architecture, BIOS version, Windows build, Intel driver version, router/AP firmware, and AP regulatory configuration.

The **Gigabyte B760M DS3H AX Rev. 1.2 + standalone Intel BE200** combination is the confirmed reference platform for the multi-channel active-connection result documented here.

## Disclaimer

This repository documents personal/laboratory test observations. It does **not** grant permission to operate on frequencies restricted in your jurisdiction. Regulatory limits differ by country and can change over time. Always follow the current rules applicable to your location and equipment.
## Credit AKHILESH KUMAR SHUKLA 
