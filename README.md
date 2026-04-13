# BBC Micro Model B – RS423 Serial Terminal to Modern PC (PuTTY)

A working guide to connect a **BBC Micro Model B (Issue 7)** to a Windows PC using the RS423 port for a full remote terminal session with **PuTTY**.

This is exactly what finally worked on my machine. 

## Hardware Used

- **BBC Micro Model B** – Issue 7 motherboard  
- **5-pin domino male plug** (inserted into BBC RS423 female socket)  
- **FTDI USB to RS232 DB9 adapter** (OIKWAN model, Amazon ASIN B0759HSLP1 – genuine FTDI chipset)  
- **DB9 female connector with screw terminals** (green terminal block version)  
- Jumper wire (soldered inside domino plug for handshake)  
- Standard hook-up wire for the 3 data lines + ground

**Photo of the finished cable (DB9 side):**

![DB9 cable with green screw terminal](cable-db9.jpg)

**Photo of the working setup:**

![BBC Micro with PuTTY terminal working](bbc-working.jpg)

## BBC RS423 Pinout (Your Machine)

Viewed from the back of the BBC, **RGB socket on the left**:
<img width="3011" height="1001" alt="image" src="https://github.com/user-attachments/assets/173a4872-7fd8-4ac1-8f78-2ac70cf3545e" />



## Final Working Wiring

<img width="170" height="226" alt="RS423" src="https://github.com/user-attachments/assets/09cbd32e-7a42-4299-95c6-854ca25eb0bd" />

**Data wires** (from domino plug to DB9 female):

| BBC Position       | BBC Signal              | DB9 Female Pin | Wire Colour (example) |
|--------------------|-------------------------|----------------|-----------------------|
| Top Left (E)       | E = RTS                 | 1              | —     Black           |
| Bottom Left (D)    | D = CTS                 | (jumper to E)  | —     Brown           |
| **Bottom Right**   | **B = TX from BBC**     | **2 (RXD)**    | —     White           |
| **Top Right**      | **A = RX to BBC**       | **3 (TXD)**    | —     Blue            |
| **Center**         | **C = GND**             | **5 (GND)**    | —     Grey            |

<img width="1439" height="1919" alt="image" src="https://github.com/user-attachments/assets/5db85d0a-de7b-46b1-aa6e-59aef8bcd622" />


## Step-by-Step Setup

1. Build the cable exactly as shown above (with the E↔D jumper).
2. Plug the domino male into the BBC RS423 port.
3. Plug the DB9 female onto the FTDI adapter.
4. Plug the USB end into your PC.

### Find the COM port
- Device Manager → **Ports (COM & LPT)** → note the **FTDI USB Serial Port (COMx)** number.

### PuTTY Configuration
- Connection type: **Serial**
- Serial line: `COMx` (your number)
- Speed (baud): **9600**
- Data bits: **8**
- Stop bits: **1**
- Parity: **None**
- Flow control: **XON/XOFF** (recommended)

Save the session.

### BBC Commands (type at the `>` prompt)

*FX 7,7     : Receive at 9600 baud
*FX 8,7     : Transmit at 9600 baud
*FX 3,5     : Output to both screen AND serial (best for normal use)
*FX 2,1     : Enable input from RS423 (PuTTY)

### Troubleshooting Tips

One direction only → check domino plug orientation or swap wires to DB9 pins 2 and 3.
No output from BBC → verify E↔D jumper is present.
Garbage characters → confirm exact 9600 baud and try Flow control = None

###

Made for the BBC Micro community
Feel free to improve and share this guide.
Last updated: April 13, 2026
BBC Model B Issue 7 • FTDI USB-RS232 • PuTTY
