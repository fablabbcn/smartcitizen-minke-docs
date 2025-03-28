# Atlas Scientific

<img src="https://live.staticflickr.com/65535/51230999551_3941affaa5_k.jpg" width="2000" height="1333" alt="Patí Científic Workshop">

The Smart Citizen firmware has built-in support for the calibration of the Atlas Scientific sensors. In order to calibrate the sensors you will need to use the [SCK Shell](/Guides/getting started/Using the Shell/).

The Smart Citizen firmware has built-in support for the calibration of some Atlas Scientific sensors. The supported sensors are:

- pH
- Electric Conductivity
- Dissolved Oxygen
- Oxidation reduction potential
- Temperature

In order to calibrate the sensors you will need to use the [SCK Shell](https://docs.smartcitizen.me/guides/getting-started/using-the-shell/).

To enable the sensors you just need to plug you board to the Smart Citizen kit aux port and reboot the Smart Citizen Kit and the sensors will be handled by the board.

!!! warning
    When calibrating **don't use the normal `read sensor` command**, this command applies temperature/salinity compensation, calibration should be done without any compensation. Instead you should use `control sensorName com,r` and that will return the raw metrics that sensor can provide. On the documentation of each sensor calibration procedure we describe the format of this metrics.

!!! info "Before we start"
    **Two important notes:**
    1. A lot of the materials from this guide are taken from [Atlas Scientific](https://atlas-scientific.com) datasheets. All credit to the well-designed images is theirs. We have integrated these probes in the Smart Citizen Kit because of their quality and good documentation. **This page is not meant to be a replacement for Atlas Scientific documents and we do not have any affiliation to Atlas Scientific**.
    2. There is also additional webinars that can support this page in more detail. Here [you can find the presentation](https://storage.smartcitizen.me/presentations/Minke-WEBINAR_WQ.pdf) and the link to the videos below:

    - [Smart Citizen Webinar - 3.1 Water sensors (Part 1)](https://www.youtube.com/watch?v=u4zUqcp17-g&list=PL33KKs9g8Y1IWsTZZmDc-46yFuuIRZEmi&index=10)
    - [Smart Citizen Webinar - 3.2 Water sensors (Part 2)](https://www.youtube.com/watch?v=aGtT2JRmkaY&list=PL33KKs9g8Y1IWsTZZmDc-46yFuuIRZEmi&index=12)
    - [Smart Citizen Webinar - 3.3 Water sensors preparation](https://www.youtube.com/watch?v=xpk4Jxd-E04&list=PL33KKs9g8Y1IWsTZZmDc-46yFuuIRZEmi&index=13)
    - [Smart Citizen Webinar - 3.4 Water sensors calibration](https://www.youtube.com/watch?v=FXsMiyONtF4&list=PL33KKs9g8Y1IWsTZZmDc-46yFuuIRZEmi&index=14)
    - [Smart Citizen Webinar - 3.5 Water sensors deployment](https://www.youtube.com/watch?v=b3ftsRNpDzA&list=PL33KKs9g8Y1IWsTZZmDc-46yFuuIRZEmi&index=15)

## Atlas PH

You need to perform a 3-point calibration with the calibration solutions. The solutions vary their pH with temperature, so make sure to check the temperature prior. **The pH value at current temperature can be found on the reference table on the calibration solution bottle - you can find it [here](#calibration-solutions-temperature)**.

!!! info "Datasheet"
    Here you can find:

    - The [consumer grade pH probe datasheet](https://files.atlas-scientific.com/consumer-grade-pH-probe.pdf)
    - The [lab grade pH probe datasheet](https://files.atlas-scientific.com/pH_probe.pdf)
    - The [pH driver datasheet](https://www.atlas-scientific.com/files/pH_EZO_Datasheet.pdf):
        - Calibration theory on page 11
        - Commands on page 52

    **Example commands**

    ```
    control ph com,r
    control ph com,cal,[mid,low,high],value
    control ph com,cal,clear
    control ph com,cal,?
    ```

### 3-point calibration

This is the order of the calibration:

1. Mid point (7.00)
2. Low point (4.00)
3. High point (10.00)

!!! warning
    Always calibrate the **mid point** first because it will erase all the previous calibrations you may have done.

!!! danger
    **Always clean the probe with distilled water between each calibration**.

#### Mid point calibration

* Put the sensor in the pH 7 calibration solution.

    ![](/assets/images/WhpJiN2.png)

2. Read the sensor **multiple times until the reading is stable**:

    ```
    control ph com,r
    6.48
    control ph com,r
    6.45
    ...
    ```

3. Issue the mid point calibration command. Remember to input the pH value of the [calibration solution at the current temperature](#calibration-solutions-temperature)

    ```
    control atlas ph com,cal,mid,[value of pH at current temperature]
    ```

    !!! info "Example at 30°C"

        ```
        SCK > control atlas ph com cal,mid,6.99
        ```

4. After this command, if you take a pH reading, the result should be 7.00 (or very close to it). You can **now remove the probe from the calibration solution and clean it**.

#### Low Point Calibration

1. Put the sensor in the pH 4.00 calibration solution (low point, the red one). **The probe needs to be in the calibration solution until you issue the calibration command**.

2. Read the sensor multiple times until the reading is stable:

    ```
    control atlas ph com,cal,mid,6.99
    ```

After this command if you take a pH reading the result should be 7.00 (or very close to it)

##### Low Point Calibration

* Repeat the procedure with the **Low point** 4.00 solution (the red one). First, read the sensor multiple times until the reading is stable:

    ```
    control ph com,r
    3.98
    control ph com,r
    3.98
    ...
    ```

3. Issue the **low point** calibration command. Remember to input the pH value of the [calibration solution at the current temperature](#calibration-solutions-temperature)

    ```
    control atlas ph com,cal,low,[value of pH at current temperature]
    ```

    !!! info "Example at 30°C"

        ```
        SCK > control atlas ph com cal,low,4.01
        ```

4. After this command, if you take a pH reading, the result should be 4.00 (or very close to it). You can **now remove the probe from the calibration solution and clean it**.

#### High Point Calibration

1. Put the sensor in the pH 10.00 calibration solution (high point, the blue one). **The probe needs to be in the calibration solution until you issue the calibration command**.

2. Read the sensor multiple times until the reading is stable:

    ```
    control atlas ph com,cal,low,4.01
    ```

##### High Point Calibration

* The same step with **High point** 10.00 calibration solution (blue). First, read the sensor multiple times until the reading is stable:

    ```
    control ph com,r
    9.84
    control ph com,r
    9.84
    ...
    ```

2. Issue the **high point calibration command**. Remember to input the pH value of the [calibration solution at the current temperature](#calibration-solutions-temperature)

    ```
    control atlas ph com,cal,high,[value of pH at current temperature]
    ```

    !!! info "Example at 30°C"

    ```
    control atlas ph com,cal,high,9.96
    ```

!!! info "Extra notes"
    The command `control com,cal,?` can be used to check the calibration status as explained on datasheet page 52. The answers can be:

    - **`?CAL,0`** → No calibration done
    - **`?CAL,1`** → One point calibration done
    - **`?CAL,2`** → Two point calibration done
    - **`?CAL,3`** → Three point calibration done

    *(not tested)* If your calibration solutions are not 4, 7 and 10, you can still use them and replace `[value of pH at current temperature]` by your values.

### Electric conductivity

The pH value of the calibration solutions is affected by temperature. Make sure you compensate according to the table below when you input the calibration value:

![](/assets/images/calibration-solutions.png)

## Atlas Conductivity

You need to perform a 3 step calibration process with a **dry point** (in air), followed by a **2-point calibration** (with the calibration solutions).

!!! info "Datasheet"
    Here you can find:

    - The [K0.1 conductivity probe datasheet](https://files.atlas-scientific.com/EC_K_0.1_probe.pdf)
    - The [K1 conductivity probe datasheet](https://files.atlas-scientific.com/EC_K_1.0_probe.pdf)
    - The [K10 conductivity probe datasheet](https://files.atlas-scientific.com/EC_K_10_probe.pdf)
    - The [driver datasheet](https://www.atlas-scientific.com/_files/_datasheets/_circuit/EC_EZO_Datasheet.pdf):

        - Calibration info on page 12
        - Calibration commands on page 55

    **Example commands**

    ```
    control conductivity com,r
    control conductivity com,K,[probeType]
    control conductivity com,K,?
    control conductivity com,cal,[dry,clear,84]
    control conductivity com,cal,low,1413
    control conductivity com,cal,high,12,880
    control conductivity com,cal,?
    ```

### 2-point calibration

This is the order of the calibration:

1. Set probe type.
2. Dry point calibration (independent of the probe type).
3. Low point calibration (calibration solution to use dependent on the probe type).
4. High point calibration (calibration solution to use dependent on the probe type).

#### Set probe type

Depending on which probe you have (check drawing for reference) you should set the probe type to K 0.1, 1.0 or 10 (new drivers have K1.0 as default):

![](/assets/images/water/atlas-ec-probe-type.png)

To set the correct probe type:

```
control conductivity com,K,1.0
```

```
control conductivity com,K,?
SCK > control conductivity com K,?
?K,1.0
```

!!! info "About the sensor"
    The **Electrical Conductivity** sensor provides four different metrics:

    * Electrical Conductivity → EC
    * Total Dissolved Solids → TDS
    * Salinity → S
    * Specific Gravity → SG

    The data is presented in order and comma separated **EC,TDS,S,SG**, for instance **0.00,0,0.00,1.000**

!!! warning "Readings are 0?"
    It is normal that if the probe type has changed (for instance, if you are using a K10 probe), that the readings are 0 after setting the probe type.

#### Dry calibration

Follow the steps below with a **dry sensor** before introducing it to the calibration solutions. You need to do this step **even if the readings in are 0**.

1. Read the sensor multiple times until the reading is stable:

    ```
    control conductivity com,r
    0.00,0,0.00,1.000
    control conductivity com,r
    0.00,0,0.00,1.000
    ...
    ```

2. Issue the dry calibration command:

    ```
    control conductivity com,cal,dry
    ```

#### Low point calibration

You can check the recommended calibration solutions for each probe on the _Probetypes_ drawing (for instance, for the K1.0 probe, the _12,880uS_ and _80,000uS_ solutions are recomended)

![](/assets/images/nendSkI.png)

1. Put the probe in the low point calibration solution. **Make sure there are no bubbles.** **The probe needs to be in the calibration solution until you issue the calibration command**.

2. Read the sensor multiple times until the reading is stable:

    ```
    control conductivity com,r
    13470,7278,7.76,1.0
    control conductivity com,r
    13230,7144,7.61,1.0
    ...
    ```

3. Issue the **low point** calibration command. **The value to input is the one of the calibration solution**, for example _12880_:

    ```
    control conductivity com,cal,low,12880
    ```

After this command readings will **not change**. **You can remove the probe from the calibration solution and rinse it now. Calibration solution can be reused.**

#### High point calibration

Repeat the steps above with **high point** calibration solution.

```
control conductivity com,cal,high,80000
```

After this steps the **two point calibration is complete** and the readings **will change**.

### Dissolved Oxygen

You have two options for this calibration:

1. Single point calibration (dry point)
2. 2-point calibration (dry point and 0 mg/l point) - **only if you need accurate readings below 1mg/l**

**Make sure you have followed the [probe reconditioning](/Guides/deployments/Water sensors/#dissolved-oxygen) before proceeding with this calibration.**

!!! info "Datasheets"
    Here you can find:

    * The [datasheet of the lab grade probe](https://files.atlas-scientific.com/LG_DO_probe.pdf)
    * The [datasheet of the mini lab grade probe](https://files.atlas-scientific.com/Mini_DO_probe.pdf)
    * The [datasheet of the driver](https://www.atlas-scientific.com/_files/_datasheets/_circuit/DO_EZO_Datasheet.pdf):
        - Calibration info on page 9
        - Calibration commands on page 52

    **Example commands** (you can put `control ox`, `control oxygen` or `control dissolved oxygen` - **however!** do not put `control dissolved` as  it will use TDS)

    ```
    control ox com,r
    control ox com,cal
    control ox com,cal,0
    control ox com,cal,clear
    control ox com,cal,?
    ```

!!! warning "Pressure compensation"
    If the sensor is going to be used more than 10 meters deep into the water **Pressure compensation** should be set with:

    ```
    control ox com,P,kPaValue
    ```

    More information on [datasheet](https://www.atlas-scientific.com/_files/_datasheets/_circuit/DO_EZO_Datasheet.pdf), page 57

### Single point calibration

!!! warning "First calibrate, compensate later"
    Temperature, salinity and pressure compensation values have no effect on calibration.

1. Read the sensor multiple times until the reading is stable.

    ```
    control ox com,r
    13.95,50%
    control ox com,r
    13.76,49%
    ...
    ```

2. Issue the calibration command, after this the readings will change. In this case, there is no need to add any value after `cal`. The sensor will take the current reading as the _dry point_.

    ```
    control ox com,cal
    ```

!!! danger "Be careful"
    If at any point of the calibration process you see akward readings (for instance, that using a 0mg/l solution for dissolved oxygen you see weirdly high values), it is better to start over. For this, proceed with:

    ```
    control ox com,cal,clear
    ```

    And start from the beginning.

### 2-point calibration

**Two point calibration is recommended if you require accurate readings below 1.0 mg/l.** After completing the single point calibration procedure put the probe in the calibration solution.

![](/assets/images/icxCaOZ.png)

1. Put the probe in the 0mg/l point calibration solution. **Make sure there are no bubbles.** **The probe needs to be in the calibration solution until you issue the calibration command**.

    !!! danger "Be careful"

        As you are calibrating the probe, oxygen is going into the solution. This calibration solution can't be reused if left open for long periods of time. Make sure you check the [driver datasheet](https://files.atlas-scientific.com/LG_DO_probe.pdf) (page 6 and 7) for more info.

2. Read the sensor multiple times until the reading is stable:

    ```
    control ox com,r
    13.95,50%
    control ox com,r
    13.76,49%
    ...
    ```

3. Issue the calibration command. In this case, you have to input the value of the calibration solution too, for example _0_:

    ```
    control ox com,cal,0
    ```

!!! info "Check the common pitfalls"
    Atlas has some interesting videos about this probe common issues:

    - [Dissolved Oxygen | Common Mistakes | Air Bubble](https://youtu.be/1I1Sk9pt47c)
    - [Dissolved Oxygen | Common Mistakes | Stagnant vs Moving Water](https://youtu.be/d9zkxkv55SE)
    - [Dissolved Oxygen | Common Mistakes | Damaged Membrane](https://youtu.be/PiXnvrTnVjs)

## Oxidation-Reduction Potential

You only need to perform a **single point calibration**. You can use any calibrated solution, as long as it's within your sensor range. Atlas Scientific uses a 225mV calibration solution.

!!! info "Datasheet"
    Here you can find:

    - The [consumer grade ORP probe datasheet](https://files.atlas-scientific.com/consumer-grade-ORP-probe.pdf)
    - The [lab grade ORP probe datasheet](https://files.atlas-scientific.com/orp_probe.pdf)
    - The [driver datasheet](https://files.atlas-scientific.com/ORP_EZO_Datasheet.pdf):
        - Calibration info on page 12
        - Calibration commands on page 49

    **Example commands**

    ```
    control redox com,r
    control redox com,cal
    control redox com,cal,[value]
    control redox com,cal,clear
    control redox com,cal,?
    ```

### Single point calibration

![](/assets/images/atlas_orp_cal_process.png)

1. Read the sensor multiple times until the reading is stable. **Make sure there are no bubbles.** **The probe needs to be in the calibration solution until you issue the calibration command**.

    ```
    control redox com,r
    225
    control redox com,r
    224
    ...
    ```

2. Issue calibration command:

    ```
    control redox com,cal,[value of ORP]
    ```

!!! info "Example at 25°C"

    ```
    control redox com,cal,225
    ```

### Temperature

You only need to perform a single point calibration. This process is only necessary if you change the probe cable or the first time you use the sensor.

!!! info "Datasheet"
    Here you can find:

    - The [PT-1000 probe datasheet](https://files.atlas-scientific.com/PT-1000-probe.pdf)
    - The [driver datasheet](https://files.atlas-scientific.com/EZO_RTD_Datasheet.pdf):
        - Calibration info on page 12
        - Calibration commands on page 53

    **Example commands**

    ```
    control atlas temp com,r
    control atlas temp com,cal
    control atlas temp com,cal,[value]
    control atlas temp com,cal,clear
    control atlas temp com,cal,?
    ```

!!! warning
    This is needed because the temperature probe is a resistive sensor – more cable → more resistance!

!!! danger "Reference"
    You will need another temperature probe or something of known temperature (like boiling water, or the triple point of water...) for this. If  you are using a reference sensor, make sure both are stable before issuing calibration commands!

### Single point calibration

* Read the **reference probe** multiple times until the reading is stable. Write down the value:

    ```
    control atlas temp com,r
    22.5
    control atlas temp com,r
    22.4
    ...
    ```

* Read the **target probe** multiple times until the reading is stable:

    ```
    control atlas temp com,r
    29.5
    control atlas temp com,r
    29.4
    ...
    ```

* Issue calibration command:

    ```
    control atlas temp com,cal,[value of temperature from reference probe or temperature]
    ```

## Factory reset procedure

!!! info "Why is this needed?"
    You may need to do a factory reset for water sensors for different reasons. However, the most common case is a wrong calibration process and it's very much related to a wrongful automatic temperature compensation of the sensor while calibrating the sensor.

    To explain further: EC, DO and pH sensor readings are automatically compensated by temperature readings. If there is an existing temperature correction in the EZO driver, or there is a correction in the middle of the calibration process, the data available for the calibration process will be invalid. Follow the steps below to be make sure there is no correction while you calibrate the probes.

Each EZO driver has it's independent calibration and status. This process needs to be done per **_driver_** (i.e. per EZO metric). To make a factory reset procedure for the EZO drivers follow the steps below:

1. Make sure that the [Smart Citizen Data](/Components/boards/Data%20Board/) board will not take any readings while you follow the calibration process. The best option is to reset the configuration to the defaults. Make sure you [back-up your information](/Guides/firmware/Update%20the%20firmware/?h=bac#make-a-back-up-of-your-info) before:

    - The config command will output your current configuration. Copy it and keep it safe:

    ```
    config
    ```

    - Then issue the default configuration:

    ```
    config -defaults
    ```

    - The LED should be red now (the Data Board is in [Setup mode](/Smart%20Citizen%20Kit/?h=setup#setup-mode))

2. Issue the factory reset command to the _driver_ in question. For instance, for the _conductivity_ one:

    ```
    control cond com factory
    0
    ```

3. Now you can check what the status of the device is:

    ```
    control cond com cal,?
    ?CAL,0
    ```

4. Reset the kit

5. Follow the calibration process as you would normally would. Remember that for _conductivity_ you may need to [re-issue the probe type](#set-probe-type)

6. Reconfigure the kit using the `config` command, by putting back the information you backed-up before:

    ```
    config -mode ...
    ```

!!! success "Ready to go?"
    If you want to send the data to the platform, you will need to register the unit using the [Advanced Kit Selection](/Guides/getting started/Onboarding Sensors/#advanced-kit-selection/). At the moment the closest Kit Blueprint will be `#22 BioPV Kit` or `#31 SCK 2.1 Sea Water` in case you are using a SCK2.1 with GPS. You can request in the [forum](http://forum.smartcitizen.me) for a custom blueprint with the specific sensors you are using.

!!! danger
    After finishing the calibration process **restart your SCK** to start from a clean state.
