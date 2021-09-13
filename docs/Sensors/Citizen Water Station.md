# Citizen Water Station

<img src="https://live.staticflickr.com/65535/51124639732_90241111a9_k.jpg" alt="Water Station - Patí Científic">

Different sensor probes can be selected for different needs. For example the setup shown above is designed for sea water measurements and includes [Atlas Scientific](https://www.atlas-scientific.com) temperature, conductivity and PH probes.

Some of the sensors selected are from Atlas Scientific, a New York-based company that _converts devices that were originally designed to be used by humans into devices that are specifically designed to be used by robots_. However, they are modular and exceptionally well documented by the manufacturer. That includes **excellent** documentation on how to install, calibrate and integrate them with additional existing hardware. In this direction, we developed a full library for the SCK to support the sensors via the _auxiliary sensor connector_. As the sensors can be configured in different ways, we do not provide a full step-by-step guide. Instead, we refer to the documentation on the [project's repository](https://github.com/fablabbcn/smartcitizen-grow/tree/master/soil-water-probes).

!!! info "Use cases"
    Check how we have used the water or soil sensors in various projects in the [Use cases section](https://docs.smartcitizen.me/Use cases/Research/)

## Hardware

<img src="https://live.staticflickr.com/65535/51232063715_5e37cfb1a0_k.jpg" width="2000" height="1333" alt="Patí Científic Workshop">

### Available measurements

The sensors described below are additional to those already supported on the [Smart Citizen Kit base sensors](https://docs.smartcitizen.me/Smart Citizen Kit/#sck-21). 

| Metric | Usage | Probe | Driver | Calibration |
| :-: |:-: |:-: |:-: |:-: |
| Temperature | Soil and water|  Atlas PT-100 + PT-1000 | Atlas EZO-RTD | Not required |
| PH | Water |  Atlas ENV-40-PH or ENV-35-PH | Atlas EZO-PH | Atlas CHEM-PH |
| PH | Soil |  Atlas ENV-45-PH | Atlas EZO-PH | Atlas CHEM-PH |
| Electrical Conductivity | Soil and water | Atlas ENV-40-EC-K | Atlas EZO-EC | Atlas CHEM-EC |
| Total Dissolved Solids | Soil and water | Atlas ENV-40-EC-K | Atlas EZO-EC | Atlas CHEM-EC |
| Salinity | Soil and water | Atlas ENV-40-EC-K | Atlas Atlas EZO-EC | Atlas Atlas CHEM-EC |
| Specific Gravity |  Soil and water | Atlas ENV-40-EC-K | Atlas EZO-EC | Atlas CHEM-EC |
| Dissolved Oxygen | Water | Atlas ENV-40-DO | Atlas EZO-DO | Atlas CHEM-DO |
| Oxygen Saturation| Water | Atlas ENV-40-DO | Atlas EZO-DO | Atlas CHEM-DO |
| Soil Moisture | Soil | Catnip Chirp! | None | Cup of water |

!!! warning "Soil and water"
    For probes that can be used in both, soil and water, make sure to [follow this procedure](https://atlas-scientific.com/files/ec_soil.pdf).

### Atlas Scientific Carrier board board 

We recommend using [Whitebox Labs Tentacle T3](https://www.whiteboxes.ch/shop/tentacle-t3-for-raspberry-pi/) that hosts up to 3 Atlas Scientific Probes, and can be stacked with several units. It connects to the SCK via the Aux sensor connector, and needs external 5V connection, which means that it can't run on battery directly connected to the SCK without extras. If you want to make your own, before the Tentacle T3 existed we designed a [custom board](https://github.com/fablabbcn/monitoring-kit-hardware) in collaboration in with [Aquapiooners](http://aquapioneers.io).

![](https://i.imgur.com/6FysvIl.png)

!!! info "Ready to set it all up"
    Visit [this guide](/Guides/deployments/Citizen Water Station/) to get started.

### Enclosures

A normal IP enclosure can be used for this setup. More information about the BOM and design files can be found [in the enclosures repository](https://github.com/fablabbcn/smartcitizen-enclosures/tree/master/Smart%20Citizen%20Water%20Station).

<img src="https://live.staticflickr.com/65535/51125200496_67b06e79bd_k.jpg" alt="Water Station - Patí Científic">

!!! info "Thanks!"
    This enclosure and development has been done in collaboration with [ICM-CSIC](https://www.icm.csic.es/en) and the [Club Pati Vela de Barcelona](https://pativelabarcelona.com/).

## Water Station

An specific Water Station was designed as part of the [Pati Scientific](https://paticientific.org/) project in colaboration with the [Institut de Ciències del Mar](https://www.icm.csic.es/en). The station currently measures the sensors below, but virtually any [supported sensor](https://docs.smartcitizen.me/Components/Auxiliary Connector/#full-list) can be added:

![](/assets/images/pativela.jpg)
_Image credit: Pati Scientific_

- Temperature
- PH
- Electrical Conductivity
- Dissolved Oxygen
- GPS location

