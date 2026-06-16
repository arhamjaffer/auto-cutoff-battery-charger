# auto-cutoff-battery-charger
 PCB-based charging circuit with automatic cut-off; optimized for safe long-term operation
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=180&section=header&text=Auto%20Cut-Off%20Battery%20Charger&fontSize=38&fontColor=ffffff&animation=fadeIn&fontAlignY=40&desc=PCB%20Design%20%7C%20KiCad%20%7C%20Smart%20Charging%20Circuit&descAlignY=62&descColor=a0aec0"/>

[![KiCad](https://img.shields.io/badge/KiCad-PCB_Design-314CB0?style=for-the-badge&logo=kicad&logoColor=white)](https://www.kicad.org/)
[![Battery](https://img.shields.io/badge/Battery-12V_Lead_Acid-F7DF1E?style=for-the-badge&logo=battery&logoColor=black)]()
[![Status](https://img.shields.io/badge/Status-Prototype_Ready-brightgreen?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)]()

</div>

---

## 📌 Overview

An **automatic battery charger with cut-off protection** — designed to safely charge a **12V lead-acid battery** and automatically disconnect when fully charged, preventing overcharging and extending battery life.

This project covers the **full PCB design cycle**: circuit design, schematic capture in KiCad, component selection, PCB layout, and fabrication-ready Gerber export.

> Designed as part of my circuit design & PCB prototyping work at NUST-PNEC.

---

## 🖼️ Board Preview

> *(Add your PCB layout screenshot or 3D render here)*

| Schematic | PCB Layout | 3D View |
|-----------|------------|---------|
| ![Schematic](images/schematic.png) | ![PCB](images/pcb_layout.png) | ![3D](images/3d_render.png) |

---

## ⚙️ Specifications

| Parameter | Value |
|-----------|-------|
| **Input Voltage** | 14–15V DC (from transformer + rectifier) |
| **Output / Charging Voltage** | 13.8V – 14.4V (12V battery) |
| **Cut-Off Voltage** | ~14.4V (fully charged threshold) |
| **Max Charging Current** | ~1A |
| **Battery Type** | 12V Lead-Acid / SLA |
| **Cut-Off Mechanism** | Comparator-based (LM358 / LM393) |
| **Indication** | LED — Charging (Red) / Full (Green) |
| **Protection** | Overcharge cut-off, Reverse polarity |
| **PCB Layers** | 2-Layer |
| **EDA Tool** | KiCad |

---

## 🔋 How It Works

```
AC Mains Input
      ↓
Transformer (Step-Down)
      ↓
Bridge Rectifier (1N4007 × 4)
      ↓
Filter Capacitor (Smoothing)
      ↓
Voltage Regulator / Charging Stage
      ↓
Comparator Circuit (LM358)
   monitors battery voltage continuously
      ↓
   Battery Voltage < 14.4V  →  Relay ON  →  Charging continues  🔴 LED
   Battery Voltage ≥ 14.4V  →  Relay OFF →  Charging stops      🟢 LED
      ↓
Battery (12V Lead-Acid)
```

The heart of this circuit is the **LM358 op-amp comparator** — it compares the battery terminal voltage against a fixed reference (set via a voltage divider using a potentiometer). When battery voltage crosses the threshold, the comparator output switches, triggering the **relay to cut off charging automatically**.

---

## 🗂️ Project Structure

```
auto-cutoff-battery-charger/
│
├── 📁 Schematic/
│   └── battery_charger.kicad_sch      # Full schematic
│
├── 📁 PCB/
│   └── battery_charger.kicad_pcb      # PCB layout
│
├── 📁 Gerbers/
│   ├── battery_charger-F_Cu.gbr       # Front copper
│   ├── battery_charger-B_Cu.gbr       # Back copper
│   ├── battery_charger-F_Silkscreen.gbr
│   ├── battery_charger-B_Silkscreen.gbr
│   ├── battery_charger-F_Mask.gbr
│   ├── battery_charger-B_Mask.gbr
│   ├── battery_charger-Edge_Cuts.gbr  # Board outline
│   └── battery_charger.drl            # Drill file
│
├── 📁 BOM/
│   └── BOM.csv                        # Bill of Materials
│
├── 📁 images/
│   ├── schematic.png
│   ├── pcb_layout.png
│   └── 3d_render.png
│
└── README.md
```

---

## 🔩 Bill of Materials

| # | Component | Value / Part | Package | Qty |
|---|-----------|-------------|---------|-----|
| 1 | Op-Amp Comparator | LM358 / LM393 | DIP-8 / SOP-8 | 1 |
| 2 | Relay | 12V SPDT | PCB Mount | 1 |
| 3 | Relay Driver Transistor | BC547 / 2N2222 | TO-92 | 1 |
| 4 | Rectifier Diodes | 1N4007 | DO-41 | 4 |
| 5 | Flyback Diode | 1N4007 | DO-41 | 1 |
| 6 | Voltage Regulator | LM7812 / LM317 | TO-220 | 1 |
| 7 | Trimmer Potentiometer | 10kΩ | 3296W | 1 |
| 8 | Resistors | 1kΩ, 4.7kΩ, 10kΩ | 0805 / TH | 6 |
| 9 | Filter Capacitor | 1000µF / 25V | Electrolytic | 1 |
| 10 | Decoupling Capacitor | 100nF | 0805 | 2 |
| 11 | LED (Charging) | Red | 3mm / 0805 | 1 |
| 12 | LED (Full) | Green | 3mm / 0805 | 1 |
| 13 | LED Resistors | 470Ω | 0805 | 2 |
| 14 | Screw Terminals | 2-pin | 5.08mm | 3 |
| 15 | Fuse Holder + Fuse | 1A | PCB Mount | 1 |

> Full BOM available in [`/BOM/BOM.csv`](BOM/BOM.csv)

---

## 🛠️ Design Workflow

```
1. Circuit Design & Hand Calculations
        ↓
2. Schematic Capture (KiCad Schematic Editor)
        ↓
3. Component Selection & Footprint Assignment
        ↓
4. Netlist Export → PCB Editor
        ↓
5. PCB Layout & Component Placement
        ↓
6. Trace Routing (Power traces wider — 1.5mm+)
        ↓
7. Design Rule Check (DRC) — 0 errors
        ↓
8. Gerber Export (Fabrication-ready)
```

---

## ⚠️ Safety Features

| Feature | Implementation |
|---------|---------------|
| **Overcharge Protection** | Relay cuts off at ~14.4V via comparator |
| **Reverse Polarity Protection** | Diode at battery input |
| **Overcurrent Protection** | Inline fuse (1A) |
| **Flyback Protection** | Freewheeling diode across relay coil |
| **Visual Indication** | Red = Charging, Green = Full |

---

## 🏭 How to Fabricate

1. Download the [`/Gerbers/`](Gerbers/) folder
2. Zip all `.gbr` and `.drl` files
3. Upload to your preferred PCB fab:
   - [JLCPCB](https://jlcpcb.com) ← recommended, cheapest
   - [PCBWay](https://www.pcbway.com)
   - [OSH Park](https://oshpark.com)
4. Recommended settings: **2 layers, 1.6mm thickness, HASL finish**

---

## 🔓 How to Open in KiCad

```bash
# Clone the repository
git clone https://github.com/arhamjaffer/auto-cutoff-battery-charger.git

# Open in KiCad
# File → Open Project → select battery_charger.kicad_pro
```

> ⚠️ Requires **KiCad 6.0 or later**. KiCad 10.0 recommended.

---

## 📸 Design Highlights

- ✅ Comparator-based automatic cut-off — no microcontroller needed
- ✅ Adjustable cut-off voltage via onboard trimmer pot
- ✅ Clear dual-LED charging status indication
- ✅ Power traces sized for current capacity (1A+)
- ✅ Proper relay flyback protection
- ✅ Screw terminals for easy battery & input connection
- ✅ Fabrication-ready Gerbers included

---

## 🧪 Testing & Calibration

Once assembled:

1. **Set cut-off voltage** — connect a bench power supply set to **14.4V**, adjust the trimmer pot until the relay clicks OFF and green LED lights
2. **Test charging** — connect a discharged 12V battery; red LED should glow and current should flow
3. **Verify cut-off** — as battery reaches full charge (~14.4V), relay should disconnect automatically
4. **Check fuse** — replace with correct 1A rating before use with mains-derived supply

> ⚡ **Warning:** If using with a mains transformer, ensure proper isolation and follow electrical safety practices. High voltage is dangerous.

---

## 🙋 Author

**Arham Jaffer**
B.E. Electrical Engineering — NUST-PNEC, Karachi 🇵🇰
Co-Founder @ [GenXi Tech Solutions](https://www.genxitechsolutions.com/)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/arham-jaffer-7911a3308)
[![Email](https://img.shields.io/badge/Email-arhamkaimkhani1949%40gmail.com-D14836?style=flat-square&logo=gmail)](mailto:arhamkaimkhani1949@gmail.com)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-Chat-25D366?style=flat-square&logo=whatsapp)](https://wa.me/923078331121)

---

## 📄 License

This project is open-source under the [MIT License](LICENSE). Feel free to use, modify, and build upon it — just give credit!

---

<div align="center">
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f3460,50:16213e,100:1a1a2e&height=100&section=footer"/>
</div>
