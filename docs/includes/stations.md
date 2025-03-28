## Station specs

### Power

Currently, the Smart Citizen Air Quality Stations have only been tested with an [external power supply](https://docs.smartcitizen.me/hardware/addons/power-supply/) (230VAC to 5VDC), with a small battery for backup during power brownouts. Due to the number of sensors, and depending on the configuration the solution is normally not meant for long term deployment with just battery power. For detailed specifications of the power supply, visit the [power supply section](https://docs.smartcitizen.me/hardware/addons/power-supply/).

| Power        |                                                                  |
| :-:          | :-                                                               |
| DC Voltage   | 5V                                                               |
| DC Current   | 2A _recommended_                                                 |
| AC Voltage   | 230V  _into the [Power Supply](https://docs.smartcitizen.me/hardware/addons/power-supply/)_   |
| AC Current   | <0.16A _into the [Power Supply](https://docs.smartcitizen.me/hardware/addons/power-supply/)_  |

!!! warning "Battery or solar operation?"
    The Station currently supports battery operation only for short periods of time (<2d days). Depending on the location, [solar power](https://docs.smartcitizen.me/hardware/addons/solar-panel/) might be available, but we do not recommend it unless you are willing to _experiment_.

### Connectivity

Similar to the [Smart Citizen Kit](https://docs.smartcitizen.me/hardware/kit/) if you want to have your data online, the Smart Citizen Air Quality Station requires a Wi-Fi connection to report data to the [platform](https://docs.smartcitizen.me/data/data-platform/). If not, the unit can also store data locally on its onboard sd-card. Read more about the [operation modes](https://docs.smartcitizen.me/hardware/kit#operation-modes) and the [supported networks](/_FAQ/#what-networks-does-it-support).