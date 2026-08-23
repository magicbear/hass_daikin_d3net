# daikin_d3net

## Overview
Home Assistant Daikin DIII-Net Modbus Integration.

Home Assistant custom component to integrate with the Daikin DTA116A51 DIII-Net/Modbus Adapter.

Developed against a VRV IV-S system, DTA116A51 and Modbus RTU/TCP gateway. 

It currently supports communication over **Modbus TCP** and **Modbus RTU** over TCP. No current support for hot water functions. Unfortunately, the DCPA01 is not supported and no documentation is available.

Enumerates units attached to DIII-Net bus, provides Climate entities for each.

## Features (1.8)

Ported from the HomePanel `daikin-485.py` DIII-NET controller, aligned with the EKMBDXB register map:

- **Ventilation / HRV (VAM)** — operation mode 4 (Vent) and ventilation subtype Auto / Energy Reclaim / Bypass (`32804` / `42404`). HomePanel called these auto / 全热换气 / 普通换气.
- **Error codes** — ASCII codes from `33601` with the HomePanel two-character message table, plus error / alarm / warning bits. Gateway-level last-error sensors match HomePanel's virtual device `0`.
- **Cool/heat master** — Master / Slave / Unknown (`32002` bits 15-14).
- **Forced off, defrost, operation status** (actual fan / heating / cooling).
- **Gateway diagnostics** — interface initialised, other DIII device present, connected unit count.

Indoor climate still uses holding `42001-42003` with the documented fan-control flag of `6`. Ventilation writes go to holding `42404` (HomePanel previously wrote the next indoor unit's power register; that address is not used here).

## Installation
Install with [HACS](https://hacs.xyz), currently as a custom repository by manually adding this repository or with the link below

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=magicbear&repository=hass_daikin_d3net&category=integration)

OR

Download this repository and place `custom_components/daikin_d3net` in the Home Assistant `config/custom_components/daikin_d3net` folder.

After rebooting Home Assistant, this integration can be configured through the integration setup UI.

## Communication Specification

Communication details are based on the [Daikin Design Guide Modbus Interface DIII](https://www.daikin-ce.com/content/dam/document-library/Installer-reference-guide/ac/vrv/ekmbdxb/EKMBDXB_Design%20guide_4PEN642495-1A_English.pdf).

## Screens

![Integration](/images/integration.png)

![Device List](/images/devices.png)

![Device Details](/images/device.png)

## Hardware

[Example DIY hardware implementation](hardware.md)
