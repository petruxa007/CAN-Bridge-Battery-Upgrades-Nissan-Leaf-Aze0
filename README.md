# Nissan LEAF Battery Module Replacement — 2-Port CAN Bridge

![Project Banner](https://github.com/dalathegreat/Nissan-LEAF-Battery-Upgrade/blob/main/Software/CANBRIDGE-2port/Banner.jpg)

Welcome! This project provides firmware and instructions for using a **2-port CAN bridge when replacing battery modules while keeping the original Nissan LEAF LBC (Lithium-ion Battery Controller)**.

Please read this documentation carefully before purchasing, flashing, or installing the hardware to ensure that this solution is suitable for your vehicle and battery configuration.

## ⚠️ Important — Read Before Using

**This firmware is intended for battery module replacement while retaining the original LBC. It is not intended for a complete battery replacement.**

There are two different scenarios:

- **Replacing battery modules while keeping the original LBC:** This is the intended use case for my firmware. It is designed for the supported 2-port CAN bridge.
- **Replacing the entire battery pack:** If you are installing a different complete battery pack, please use Dala's Nissan LEAF Battery Upgrade project instead. It is a separate solution intended for battery upgrades.

👉 **Dala's project:** [Nissan LEAF Battery Upgrade — Repository Link](https://github.com/dalathegreat/Nissan-LEAF-Battery-Upgrade?tab=readme-ov-file)

Before proceeding, make sure you understand the differences between battery module replacement, complete battery replacement, the LBC, and CAN communication.

For additional background information, you can also consult the [Nissan LEAF Battery Upgrade Wiki](https://github.com/dalathegreat/Nissan-LEAF-Battery-Upgrade/wiki).

> **Compatibility notice:** This project supports the specified 2-port CAN bridge only. Three-port CAN bridges are not supported by this firmware.

## 💻 Firmware Purchase

This firmware is a paid project. I do not distribute my compiled firmware for free. However, I keep the price reasonable and affordable to reflect the work involved in developing, testing, and maintaining it.

### What you get

- Firmware for the supported 2-port CAN bridge.
- **Free firmware updates for everyone who has purchased the firmware.** You will not need to pay again for future updates to this firmware.
- Direct contact for purchase-related questions and technical consultations.

**Purchase the firmware:**

👉 [Buy the Firmware — Purchase Link](https://example.com/your-firmware)

Prefer to purchase directly or have questions before buying?

📧 **Email:** your-email@example.com

Feel free to contact me for purchase inquiries, compatibility questions, or consultation before starting your installation.

Please include your vehicle model, model year, battery configuration, and CAN bridge version when asking for technical assistance.

## 🔧 Required Hardware

This firmware is designed for the supported **2-port Budget CAN bridge**.

| Hardware | Details |
|---|---|
| CAN bridge | 2-port CAN bridge, blue PCB version |
| Programmer | ST-Link V2 |
| Connection | SWD programming interface |

**Important:** For the 2-port CAN bridge, use the **BLUE PCB version**. Other board variants are not supported unless explicitly confirmed to be compatible.

### Where to buy the CAN bridge

[Search for the 2-port CAN bridge on AliExpress](https://www.aliexpress.com/w/wholesale-MB-CAN-Filter-18-in-1.html)

Check the PCB version and hardware compatibility before purchasing.

## 🛠️ Software Required for Flashing

| Software | Purpose | Download |
|---|---|---|
| STM32 ST-LINK Utility | Flashing the 2-port CAN bridge | [Download from ST](https://www.st.com/en/development-tools/stsw-link004.html) |
| ST-LINK CLI | Command-line programming support | Included with the STM32 ST-LINK Utility installation |
| VC++ 2015 x86 Redistributable | Runtime dependency for BridgeFlasher.exe, if required | [Download from Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=48145) |

## 🔌 Hardware Required for Flashing

You will need an **ST-Link V2 programmer** to flash the supported CAN bridge.

[Find an ST-Link V2 programmer on eBay](https://www.ebay.com/sch/i.html?_nkw=ST-Link+V2)

Programmer clones may differ in their pinout and operation, so verify the labels on your particular device before connecting it.

## ⚙️ Flashing Instructions

### Step 1 — Prepare the programmer

Install the STM32 ST-LINK Utility and connect your ST-Link V2 programmer to your computer.

### Step 2 — Connect the programmer to the CAN bridge

Connect the ST-Link V2 to the J1 programming header on the 2-port CAN bridge.

Dupont wires can be difficult to connect securely to the small PCB pads. Needle probes may make the connection easier.

Follow the pin labels on your programmer rather than relying on the physical position of the pins, as layouts can vary.

| ST-Link V2 Pin | CAN Bridge Connection |
|---|---|
| Pin 7 — 3.3V | J1 |
| Pin 3 — GND | J3 |
| Pin 2 — SWDIO | J4 |
| Pin 6 — SWCLK | J5 |
| Not connected | J2 |

Double-check every connection before powering or programming the board.

### Step 3 — Flash the firmware

Use `BridgeFlasher.exe` from the software folder and select the appropriate firmware file supplied with your purchase.

If you use ST-LINK CLI, configure the flashing utility to point to `ST-LINK_CLI.exe` in the STM32 ST-LINK Utility installation directory.

If `BridgeFlasher.exe` fails to start, install the [Microsoft Visual C++ 2015 x86 Redistributable](https://www.microsoft.com/en-us/download/details.aspx?id=48145).

### Step 4 — Confirm successful programming

Start the flashing process and wait for the programmer to report successful completion.

Do not install the bridge in the vehicle until programming has completed successfully.

**Flashing demonstration:** [Watch the 2-port CAN bridge flashing video](https://www.youtube.com/watch?v=LssrvVYLtp8)

## 🚗 Installing the 2-Port CAN Bridge

When installing the bridge in the vehicle, identify each wire using the labels on the back of the PCB. Wire colors can vary between production batches.

The following connections describe the general wiring arrangement for the supported bridge:

| CAN Bridge Wire / Label | Vehicle Connection |
|---|---|
| Red wire #1 | Constant +12V, protected by a 3A fuse |
| Red wire #2 | Constant +12V, protected by a 3A fuse; join with the other red wire as specified by the wiring design |
| CAN-1L | Battery-side EV-CAN Low |
| CAN-1H | Battery-side EV-CAN High |
| CAN-2L | Vehicle-side EV-CAN Low |
| CAN-2H | Vehicle-side EV-CAN High |
| Black wire | Ground |
| Black wire | Ground |

**Important installation precautions:**

- Verify CAN High and CAN Low connections before powering the system.
- Confirm that both power connections and ground connections are secure.
- Protect the power supply with the specified fusing.
- Follow the actual PCB labels rather than assuming that wire colors are universal.
- If you are uncertain about the wiring or vehicle compatibility, seek qualified assistance before installation.

### Example: 2012 Nissan LEAF

[View the example installation image](https://github.com/dalathegreat/Nissan-LEAF-Battery-Upgrade/blob/main/Software/CANBRIDGE-2port/Install2012.jpg)

This image is provided as a general wiring reference. Verify the wiring for your own vehicle before proceeding.

## 🧰 Troubleshooting

### Problems flashing the CAN bridge?

If the programmer fails to connect, you see an error such as `Unable to open file!`, or the flashing application will not launch, check the following:

- Ensure that the programming connections are correct.
- Check that only the required programming connections are attached during flashing.
- Verify that the selected firmware file is correct and accessible.
- Install the required [VC++ 2015 x86 Redistributable](https://www.microsoft.com/en-us/download/details.aspx?id=48145), if needed.
- Try another USB port, USB cable, or computer if the problem persists.

### No battery information on the instrument cluster?

If the instrument cluster displays `---` instead of battery information, CAN communication through the bridge may not be working correctly.

Check the following:

- Confirm that the firmware was programmed successfully.
- Verify the CAN High and CAN Low connections on both sides of the bridge.
- Check that the bridge receives a stable, constant +12V supply and has a reliable ground connection.
- Inspect the wiring for loose connections, incorrect pin assignments, or damaged wires.

If the problem persists, stop troubleshooting and verify the installation before continuing to operate the vehicle.

## 💻 Modifying the Source Code

If you intend to modify and recompile the firmware, the development environment used for the project is:

- Keil µVision 5

Please note that modifying the source code requires appropriate embedded development knowledge and hardware debugging experience.

## 📖 Alternative Projects and Resources

If your project involves a complete battery pack replacement rather than replacing modules while retaining the original LBC, please consult the appropriate alternative project:

- **Dala's Nissan LEAF Battery Upgrade:** [Repository Link](https://github.com/REPLACE-WITH-DALA-REPOSITORY)

This project is separate from my firmware and is intended for a different use case. Please review its documentation to determine whether it suits your vehicle and battery configuration.

## 💬 Contact and Support

Have questions about compatibility, purchasing the firmware, or getting started?

You can contact me directly:

- **Email:** your-email@example.com
- **Purchase page:** https://example.com/your-firmware

When contacting me, please provide as much relevant information as possible, including your vehicle model, model year, current battery configuration, and the hardware you intend to use.

I will do my best to help you determine whether this firmware is appropriate for your setup.

## 🔄 Firmware Updates

All customers who have purchased this firmware are entitled to **free updates for this firmware**.

I believe customers should benefit from ongoing improvements without having to purchase the same firmware again. Future updates to the purchased firmware will therefore be provided at no additional cost.

For information about obtaining an update, please contact me using the email address above.

## ⚠️ Disclaimer

This project involves modifications to vehicle battery communication systems. Incorrect wiring, incompatible hardware, or improper installation can result in vehicle faults, battery communication problems, or damage to electronic components.

Always verify hardware compatibility and wiring before installation. Work on high-voltage battery systems should only be performed by appropriately qualified personnel.

This firmware is intended for the specific use case described in this documentation. It is not a universal battery upgrade solution and should not be used outside its stated compatibility without prior verification.

By purchasing or using this firmware, you are responsible for ensuring that your hardware, vehicle, and installation meet the applicable technical and safety requirements.
