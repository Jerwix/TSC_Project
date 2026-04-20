# InkTime — Open Source Smartwatch

> Proiect realizat în cadrul cursului **TSC (Tehnica Sistemelor de Calcul)**, Politehnica București, 2026.

---

## Descriere

InkTime este un smartwatch ieftin și open source bazat pe microcontrollerul **nRF52840**, echipat cu un display e-paper, senzor IMU, fuel gauge, driver haptic și comunicație wireless Bluetooth. Acest repository conține fișierele hardware complete pentru producția în masă a dispozitivului.

---

## Diagramă Bloc

```
                        ┌─────────────────────────────────────────┐
                        │              nRF52840 (U2)               │
                        │           Microcontroller MCU            │
                        └──┬──────┬──────┬──────┬──────┬──────┬───┘
                           │      │      │      │      │      │
                  I2C    SPI    GPIO   GPIO   I2C    I2C   GPIO
                   │      │      │      │      │      │      │
              ┌────┘  ┌───┘  ┌───┘  ┌───┘  ┌───┘  ┌───┘  ┌───┘
              │       │      │      │      │      │      │
         ┌────▼──┐ ┌──▼───┐ ┌▼───┐ ┌▼───┐ ┌▼────┐ ┌▼────┐ ┌▼────┐
         │BMA423 │ │E-Paper│ │SW  │ │ANT1│ │MAX  │ │DRV  │ │IC1  │
         │  IMU  │ │Display│ │Butt│ │2.4G│ │17048│ │2605 │ │BQ   │
         │(IC3)  │ │ (J1)  │ │ons │ │Hz  │ │Fuel │ │Haptic│ │25180│
         └───────┘ └───────┘ └────┘ └────┘ │Gauge│ │Drvr │ │LiPo │
                                            │(U1) │ │(IC4)│ │Chgr │
                                            └─────┘ └─────┘ └──┬──┘
                                                                │
              ┌─────────────────────────────────────────────────┘
              │
         ┌────▼──┐     ┌────────┐     ┌──────────┐
         │RT6160 │     │USB-C   │     │ Li-Po    │
         │DC/DC  │◄────│(J2)    │     │ Battery  │
         │(IC2)  │     │KH-TYPE │     │ 3.7V     │
         └───────┘     │C-16P   │     └──────────┘
                       └────────┘
```

---

## Bill of Materials (BOM)

| Qty | Referință | Componentă | Descriere | Mouser | JLCPCB |
|-----|-----------|-----------|-----------|--------|--------|
| 1 | U2 | NRF52840_QF | nRF52840 Microcontroller BLE 5.0 | - | - |
| 1 | IC1 | BQ25180YBGR | Charger IC LiPo/LiFe 8-DSBGA, 0.5mm | [Mouser](https://www.mouser.co.uk/ProductDetail/Texas-Instruments/BQ25180YBGR?qs=doiCPypUmgEWjAK%252BJAX6Tw%3D%3D) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | IC2 | RT6160AWSC | Buck-Boost DC/DC I2C, 15-WL-CSP, 0.6mm | [Mouser](https://www.mouser.co.uk/ProductDetail/Richtek/RT6160AWSC?qs=amGC7iS6iy%2FLd9PSoixZXQ%3D%3D) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | IC3 | BMA423 | Accelerometru triaxial 12bit, IMU | [Mouser](https://www.mouser.co.uk/ProductDetail/Bosch-Sensortec/BMA423?qs=HXFqYaX1Q2xC%252BSgeGoX3mg%3D%3D) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | IC4 | DRV2605YZFR | Haptic Driver ERM/LRA, BGA9 | [Arrow](https://www.arrow.com/en/products/drv2605yzfr/texas-instruments?region=nac) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | U1 | MAX17048G+T10 | Fuel Gauge 1-Cell ModelGauge, TDFN-8 | [SnapEDA](https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | J2 | KH-TYPE-C-16P | Conector USB Type-C 16 pini | [SnapEDA](https://www.snapeda.com/parts/KH-TYPE-C-16P/Kinghelm/view-part/?ref=eda) | - |
| 1 | J3 | 503480-2400 | Conector FPC 0.5mm 24 pini E-Paper, 1.87mm | [Mouser](https://www.mouser.co.uk/ProductDetail/Molex/503480-2400?qs=OAhjpuo3Vu7efIoxFh9AOw%3D%3D) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | J1 | TC2030-IDC | Conector SWD Tag-Connect 6 pini, 19mm | - | - |
| 1 | ANT1 | 2450AT18B100E | Antenă 2.45GHz SMD, 1.4mm | [Mouser](https://www.mouser.co.uk/ProductDetail/Johanson-Technology/2450AT18B100E?qs=yCnrNFeXz%252Bh5MFsFIXGZGA%3D%3D) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | D1 | USBLC6-2SC6Y | Diodă ESD USB, TVS SOT-23-6 | [SnapEDA](https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=eda) | [JLCPCB](https://jlcpcb.com/parts) |
| 3 | D2, D3, D4 | MBR0530 | Diodă Schottky 30V 500mA, SOD-123 | [SnapEDA](https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | Q1 | SI1308EDL-T1-GE3 | N-Channel MOSFET 30V 1.5A, SC-70 | [SnapEDA](https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay+Siliconix/view-part/?ref=eda) | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | Q2 | 20V/4.2A/52mΩ/1.4W | P-Channel MOSFET, SOT-23 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | X1 | 32MHz Crystal | Crystal SMD 2016, 32MHz | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | X2 | 32.768kHz Crystal | Crystal SMD 3215, 32.768kHz RTC | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | L1 | FTC252012SR47MBCA | Inductor 0.47µH SMD 2016, TDK | - | [JLCPCB](https://jlcpcb.com/partdetail/6763488-FTC252012SR47MBCA/C5832368) |
| 1 | L2 | 68µH | Inductor generic chip 0402 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | L3 | FTC252012SR47MBCA (10µH) | Inductor SMD 2016, TDK | - | [JLCPCB](https://jlcpcb.com/partdetail/6763488-FTC252012SR47MBCA/C5832368) |
| 1 | L4 | FTC252012SR47MBCA (15µH) | Inductor SMD 2016, TDK | - | [JLCPCB](https://jlcpcb.com/partdetail/6763488-FTC252012SR47MBCA/C5832368) |
| 1 | L5 | FTC252012SR47MBCA (3.9nH) | Inductor RF SMD 2016, TDK | - | [JLCPCB](https://jlcpcb.com/partdetail/6763488-FTC252012SR47MBCA/C5832368) |
| 3 | SW_UP, SW_ENT, SW_DN | EVP-AKE31A | Buton tactil SMD Panasonic | - | [JLCPCB](https://jlcpcb.com/parts) |
| 6 | R1, R9, R10, R11, R12, R15 | 10kΩ | Rezistență SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 2 | R4, R5 | 3.3kΩ | Rezistență SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 2 | R7, R8 | 5.1kΩ | Rezistență SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 3 | R2, R3, R6 | 0Ω | Rezistență SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | R13 | 0.47Ω | Rezistență SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | R14 | 2.2Ω | Rezistență SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 10 | C5,C8,C9,C10,C13,C21,C30,C34,C43,C44 | 100nF | Condensator SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 16 | C1,C3,C11,C14,C15,C16,C19,C20,C22,C23,C24,C25,C26,C27,C28,C31 | 1µF | Condensator SMD 0402 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 3 | C2, C4, C18 | 10µF | Condensator SMD 0402 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 2 | C6, C7 | 22µF | Condensator SMD 0402 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 5 | C12,C29,C45,C46,C47 | 4.7µF | Condensator SMD 0402 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | C17 | 4.7µF/25V | Condensator SMD 0402 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 4 | C35,C36,C48,C49 | 12pF | Condensator SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | C37 | 100pF | Condensator SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | C32 | 47nF | Condensator SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 1 | C42 | 820pF/NC | Condensator SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 2 | C39, C40 | 1pF | Condensator SMD 0201 | - | [JLCPCB](https://jlcpcb.com/parts) |
| 3 | C33, C38, C41 | NC | Condensator SMD 0201 (nemontate) | - | - |
| 12 | TP_3.3V, TP_3V3, TP_GND, TP_OUT+, TP_OUT-, TP_RESET, TP_SWCLK, TP_SWDIO, TP_SWO, TP_VBAT, TP_VBAT_GND, TP_VREG | Test Pad | Test pad circular 2mm | - | - |
| 1 | SJ2 | Solder Jumper | SMD Jumper | - | - |

---

## Descriere Hardware

### Microcontroller — nRF52840 (U2)

Creierul dispozitivului este **Nordic Semiconductor nRF52840**, un SoC ARM Cortex-M4 la 64MHz cu:
- Bluetooth 5.0 / BLE integrat
- 1MB Flash, 256KB RAM
- Antenă externă 2.4GHz conectată prin filtru LC (L5, C39, C40, C41, C42) la ANT1
- Cristal principal 32MHz (X1) pentru clock RF
- Cristal RTC 32.768kHz (X2) pentru timekeeping
- Alimentare 3.3V de la IC2 (DC/DC)

**Constrângere importantă:** Antena ANT1 este plasată la marginea plăcii, iar PCB-ul este decupat sub antenă — nu există cupru sau trasee sub zona antenei.

### Alimentare

Lanțul de alimentare funcționează astfel:

**USB-C (J2)** → **D1 (ESD)** → **IC1 BQ25180 (LiPo Charger)** → **Baterie LiPo 3.7V**

**Baterie** → **IC2 RT6160 (Buck-Boost DC/DC)** → **3.3V** → toată placa

IC2 este un convertor buck-boost controlat prin I2C care menține tensiunea stabilă la 3.3V indiferent de nivelul bateriei (3.0V - 4.2V).

### Display E-Paper — J1

Conectorul FPC J1 (503480-2400, 24 pini, pas 0.5mm) leagă display-ul e-paper la nRF52840 prin **SPI**:
- **EPD_MOSI** → pin AD20
- **EPD_SCK** → pin AC21
- **EPD_CS** → pin AD16
- **EPD_DC** → pin AD10
- **EPD_RST** → pin AC11
- **EPD_BUSY** → pin AD12

Circuitul de drive al e-paper-ului (diodele D2, D3, D4 și tranzistoarele Q1, Q2) generează tensiunile necesare pentru actualizarea display-ului (VGHL pozitiv și negativ).

### IMU — BMA423 (IC3)

Accelerometrul Bosch BMA423 comunică prin **I2C** cu nRF52840:
- **SDA** → pin L1
- **SCL** → pin R1
- **INT1** → pin N1
- **INT2** → pin P2

Folosit pentru detecția pașilor, orientare și gesturi.

### Fuel Gauge — MAX17048 (U1)

Monitorizează nivelul bateriei prin **I2C**:
- **SDA** → pin L1 (shared I2C bus)
- **SCL** → pin R1 (shared I2C bus)
- **ALERT** → pin U1

### Haptic Driver — DRV2605 (IC4)

Driver pentru motor haptic (vibrator), controlat prin **I2C**:
- **SDA** → pin L1
- **SCL** → pin R1
- **EN** → pin G1
- **OUT+** → motor haptic
- **OUT-** → motor haptic

### SWD — J5 (TC2030-IDC)

Conector Tag-Connect pentru programare și debugging:
- **SWDIO** → pin AC24
- **SWCLK** → pin AA24
- **SWO** → pin AD22
- **RESET** → pin AC13
- **3V3** → alimentare
- **GND** → masă

### Butoane

Trei butoane tactile Panasonic EVP-AKE31A:
- **SW_UP** → pin W24
- **SW_ENT** → pin U24
- **SW_DN** → pin R24

Fiecare buton are rezistență pull-up de 10kΩ la 3.3V și condensator de debounce.

---

## Pinout nRF52840

| Pin nRF52840 | Semnal | Componentă |
|---|---|---|
| AD20 | MOSI (EPD) | J1 pin 14 |
| AC21 | SCK (EPD) | J1 pin 13 |
| AD16 | CS (EPD) | J1 pin 12 |
| AD10 | DC (EPD) | J1 pin 11 |
| AC11 | RST (EPD) | J1 pin 10 |
| AD12 | BUSY (EPD) | J1 pin 9 |
| L1 | SDA (I2C) | IC1, IC2, IC3, IC4, U1 |
| R1 | SCL (I2C) | IC1, IC2, IC3, IC4, U1 |
| N1 | IMU INT1 | IC3 |
| P2 | IMU INT2 | IC3 |
| G1 | HAPTIC EN | IC4 |
| K2 | PMIC INT | IC1 |
| U1 | FUEL ALERT | U1 |
| W24 | BUTTON UP | SW_UP |
| U24 | BUTTON ENT | SW_ENT |
| R24 | BUTTON DN | SW_DN |
| AC24 | SWDIO | J5 |
| AA24 | SWCLK | J5 |
| AD22 | SWO | J5 |
| AC13 | RESET | J5, TP_RESET |
| AD6 | D+ (USB) | D1 |
| AD4 | D- (USB) | D1 |
| AD2 | VBUS detect | J2 |
| H23 | RF (Antenna) | ANT1 via L5 |

---

## Specificații PCB

| Parametru | Valoare |
|---|---|
| Dimensiuni | 46mm × 35mm |
| Număr layere | 2 (Top + Bottom) |
| Grosime PCB | 1mm |
| Lățime trasee semnal | min 0.15mm |
| Lățime trasee putere | 0.3mm |
| Plan de masă | TOP și BOTTOM |
| Finish suprafață | HASL Lead-Free |

---

## Decizii de Design

- **Antena ANT1** este plasată sub U2 (nRF52840), aproape de marginea plăcii, cu decupaj în planul de masă sub ea pentru performanță RF optimă.
- **Toate componentele** sunt plasate exclusiv pe layerul TOP conform specificațiilor.
- **Condensatoarele de decuplare 100nF** sunt plasate cât mai aproape de pinii de alimentare ai fiecărui IC.
- **Via stitching** aplicat între planurile de masă TOP și BOTTOM, în special în zona circuitului radio.
- Erorile de tip "Pad-Solid Polygon" la butoanele EVP-AKE31A provin din footprint-ul din bibliotecă și au fost aprobate — nu reprezintă erori de design.
- Erorile de tip "Dimension" cauzate de amplasarea butoanelor și mufei USB sunt neglijate conform observațiilor din enunț.
- Rutarea a fost realizată cu autorouter (96.6%) + corecții manuale pentru traseele rămase.

---

## Structura Repository

```
TSC_Project/
├── hardware/
│   ├── InkTime_2D.fbrd
│   ├── Schematic.fsch
│   └── Screenshot 2026-04-20 164634.png
├── manufacturing/
│   ├── bill of materials.csv
│   └── pick and place.csv
├── mechanical/
│   ├── 3D.png
│   └── InkTime_3D (Assembly).f3z
├── LICENSE
└── README.md
```

---

## Licență

Acest proiect este licențiat sub **Apache License 2.0** — vezi fișierul [LICENSE](LICENSE) pentru detalii.

---

*Proiect realizat de **Vlad** — TSC 2026, Politehnica București*
