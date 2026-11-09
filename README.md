# 5-Stage Current-Starved Ring VCO in ASAP7 7 nm

A 0.7 V ring VCO designed in Cadence Virtuoso and simulated in Spectre using the predictive ASAP7 FinFET PDK. The baseline tunes from **124 to 773 MHz** at **1.8–8.7 µW**. Simplifying the shared bias network improved the simulated phase-noise figure of merit (FoM) by **about 10 dB**.

## Why current starving?

A plain ring oscillator's frequency depends on its inverter delays. Current-starving transistors limit how quickly each stage charges and discharges, giving a PLL a separate control voltage to tune frequency while keeping the supply fixed. The extra devices consume voltage headroom, and noise on a shared bias can affect every stage.

## Circuit and sizing

The circuit uses five current-starved inverter stages and two output buffers. Each inverter device uses **8 fins**, while each current-starving device uses **1 fin**. In the initial sizing, the starving devices had only **20–33 mV** across them and operated in triode. Increasing the inverter fin count reduced the voltage dropped across the inverter devices. Together with an ideal **16 kΩ source-degeneration resistor** in the baseline bias network, this helped keep the starving devices in saturation across most of the baseline tuning window.

## Simulation results

| Metric | Result |
| --- | --- |
| Supply voltage | 0.7 V |
| Baseline tuning range | 124–773 MHz |
| Baseline power across tuning range | 1.8–8.7 µW |
| Phase noise at 1 MHz offset | −69.9 dBc/Hz baseline; −75.6 dBc/Hz redesigned bias |
| Phase-noise FoM improvement | About 10 dB |

The phase-noise values are reported at their respective simulated operating points. All results are from **schematic-level, pre-layout simulations**. Nominal simulations used the TT corner at 27 °C.

## What the noise analysis changed

Spectre PSS/Pnoise analysis attributed about **75% of the baseline phase-noise contribution** to the shared bias network. In the redesigned circuit, we removed the second bias leg and its associated degeneration resistor, then drove the NMOS current-starving gates directly from the control voltage. The ring, device sizing, and output buffers stayed the same.

The redesigned bias improved the FoM but narrowed the tuning window. Average VCO gain increased from about **5.0 to 8.9 GHz/V**, so a given disturbance on the control voltage produces a larger frequency shift. At the same nominal frequency, the simulated spread across process, voltage, and temperature (PVT) was roughly twice as large. For PLL use, the choice depends on both oscillator noise and the tuning margin needed across corners.

## Team

Sonakshi Agrawal, E. Vyshnavi, Katakam Shrihita, and Misha Maria Tomy · VIT Chennai
