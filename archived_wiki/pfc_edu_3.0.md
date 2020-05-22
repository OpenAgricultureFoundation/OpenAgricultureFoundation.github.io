---
layout: bootstrap
---
# [Archive of wiki.openag.media.mit.edu](index.md)
`Archived Contents from the original OpenAg Wiki (from archive.org snapshot on Apr 8, 2020)`

## Personal Food Computer 3.0 (PFC_EDU)
The OpenAg™ Personal Food Computer 3.0 (PFC_EDU) is the latest evolution of the [Personal Food Computer](personal_food_computers.md).

![Image of PFC-EDU 3.0](/static/images/wiki/pfc_edu_low-res_.jpg)

The PFC 3.0 (PFC_EDU)The PFC_EDU was designed by the [MIT Open Agriculture Initiative (archive.org link)](https://web.archive.org/web/20190723192227/https://www.media.mit.edu/groups/open-agriculture-openag/overview/), in collaboration with the OpenAg 
community, especially educators working in both informal and formal education settings (e.g. libraries, schools, 
museums). It can be built, used, modified and hacked by the community for any number of applications. MIT continues 
to test its functionality, design, user interface and impact on learning with our education partners [i2 Learning](https://i2learning.org), 
the [Media Lab Learning Initiative](https://learn.media.mit.edu/), and educators and nerdfarmers of various ages, technical backgrounds, and access 
to resources.

Like any [Food Computer™](index.md), the PFC_EDU is a controlled environment agriculture technology platform that uses robotic 
systems to control and monitor climate, energy, and plant growth inside its specialized growing chamber. The PFC_EDU 
design has been scaled down from previous versions of the PFC in cost, size and complexity, and offers a spectrum of 
control so that users can make their growing experience as manual or as automated as they would like.

Design decisions for the PFC_EDU were based on cost, ease of manufacture, improved data validity, testing in schools, 
libraries, and museums, as well as feedback from the community. We involved an PFC_EDU Advisory Board comprised of 
folks from across the US, with a range of backgrounds and experience using novel STEM technology tools, to help us 
understand what design features were most engaging and useful for educators working with nerdfarmers between 8 and 14 
years old.

But the PFC_EDU isn't just for educators! Their insights and recommendations helped design a small, engaging, modular 
Food Computer that nerdfarmers with a broad spectrum of skills, resources, and interests can build and use, for a wide 
variety of scientifically rigorous, citizen-science experimentation.

### New Shape
Its “3U” form factor (30cm3 / 12in3) is comparable to [NASA's Veggie Production System](https://www.nasa.gov/mission_pages/station/research/experiments/383.html), and compatible with the 
[Growing Beyond Earth Challenge STEM Education Program](https://informal.jpl.nasa.gov/museum/CP4SMP/growing-beyond-earth-challenge-stem-education-program).

### New Brain & Central Nervous System
Internally it runs our embedded software (the OpenAg Brain) on a robust [Beaglebone black wireless (BBB)](https://beagleboard.org/black-wireless) and the 
custom Central Nervous System (CNS) circuit board reads sensor data and controls LEDs to create, edit or maintain 
the [Climate Recipe](recipe.md) running inside. Nerdfarmers have the option of adding more advanced sensors and peripherals 
(pH, EC, DO, water temperature, and a USB camera) to the baseline CNS, as their skill level and resources allow.

### New Interfaces & Cloud Backend
There are a new set of cloud services (the OpenAg Cloud) that support the backend of the PFC_EDU, and connect it to 
the [Open Phenome (archive.org link)](https://web.archive.org/web/20190720114223/https://www.media.mit.edu/projects/open-phenome-project/overview/) (OpenAg's open source, digital library of Food Computer data and Climate Recipes).

The PFC_EDU also has a new web-based, front-end interface as well as a new device UI, for advanced networking, 
remote troubleshooting and monitoring. As of Fall 2018, both are still in development and testing with libraries 
and schools in a pilot test in the Boston area. You can get a sneak peak at both by taking a look at the 
Configuration Guide, below.

## Get Started
Watch the Welcome Video and see the documentation below for more details, and be sure to join the 
[OpenAg Forum (currently down)]() or [follow us on Twitter](https://twitter.com/mitopenag) to get updates from the 
community on all things PFC_EDU.

*Protip - If you're new to wiki, be sure to ctrl-click (Windows) or cmd-click (Mac) links to open them in a new tab.*

### Videos & Support Materials

- [Welcome to the PFC_EDU (youtube video)](https://youtu.be/-J1DNp4M_1k)
- [Final Assembly Guide (created with i2 Learning for Fall 2018 Pilot Test) (MISSING PDF file)]()
- [Configuration Guide (created with i2 Learning for Fall 2018 Pilot Test) (MISSING PDF file)]()
- ["Get Growing" Germination Guide  (MISSING INFORMATION)]()

## PFC_EDU Bill of Materials and Design
![pfc-edu_assembly_img.png](/static/images/wiki/pfc-edu_assembly_img.png)
![pcba_drawing.jpg](/static/images/wiki/pcba_drawing.jpg)
![brain_board_img_.png](/static/images/wiki/brain_board_img_.png)

The files you'll need to build a PFC_EDU from scratch are below:

* [PFC 3.0 (PFC_EDU) Specifications Sheet (MISSING PDF)]()
* [PFC_EDU Assembly Bill of Materials (total unit BOM, Google spreadsheet) (archive.org link)](https://web.archive.org/web/20190723192227/https://docs.google.com/spreadsheets/d/1c2H4cPmi8jmzXLx5jP24l9h5RykYYzeQhTub-tl5C-M/edit?usp=sharing)

A baseline PFC 3.0 can be assembled for about $500 with the raw materials below. 
For folks who want to outsource more advanced components to professional manufacturers, see “Getting parts of a PFC_EDU 
manufactured” below.

1. Main chassis (frame cut by CNC)
2. Water reservoir (laser cut or vacuum-formed)
3. Air stone and hose
4. A completed “Central Nervous System” (CNS), which includes a printed circuit board (PCB) and
    - BeagleBone Black
    - LED lights
    - Fans
    - Temperature, humidity and C02 sensors
    - Air pump
    - USB camera
    - Power supply and cord
    - For more advanced environmental data, the PFC_EDU CNS can be modified to include these optional sensors:
        - EC probe (a conductivity sensor for nutrient concentration)
        - pH probe
        - Water temperature probe

## Software
All the details for getting your BeagleBone Black ready, software installed, configured and updated are available in the ReadMe's at the links below.

 - [OpenAg Brain (Django/Python)](https://github.com/OpenAgricultureFoundation/openag-device-software)
 - [OpenAg Cloud (Python/React/Flask)](https://github.com/OpenAgricultureFoundation/self_hosted_backend)
    - `Note the 'OpenAg Cloud' now points to a self hosted docker based option`
    
![OpenAg Cloud Architecture](/static/images/wiki/openag_cloud_arch_v4_small.jpg)

[OpenAg Cloud Architecture Description](https://github.com/OpenAgricultureFoundation/Data_API/blob/master/docs/OpenAg%E2%84%A2%20Cloud%20Description%20v4.pdf)

`NOTE: The Architecture described above was the original Google Cloud Platform based backend. The new 'self_hosted_backend' 
will have a description in it's repository's readme`

## Hardware
### Electrical
Files for circuit board, sensors, and actuators (“central nervous system”)

 - [Circuit Board Design files & Assembly Bill of Materials](https://github.com/OpenAgricultureFoundation/openag-electrical/tree/master/prj/pfc-edu/v4.0)
 - [Optional Sensors Bill of Materials* (Google Spreadsheet) (MISSING DATA)]()

*note: CO2 and environmental temperature/humidity sensors are included in the baseline CNS BOM. The pH, EC, water 
temperature and camera are optional and included in the Optional Sensors BOM.*

### Mechanical/Frame
#### Files for the chassis

 - [Chassis design files](https://github.com/OpenAgricultureFoundation/openag-mechanical/tree/master/prj/pfc-edu/v4.0) and [Bill of Materials](https://github.com/OpenAgricultureFoundation/openag-mechanical/blob/master/prj/pfc-edu/v4.0/pfc_edu%20bom.csv) (`NOTE: the original google sheets BOM with links is missing`)
 - [Chassis Manufacturing Key (chassis parts' cutting specifications, parts data, and file locations)](https://github.com/OpenAgricultureFoundation/openag-mechanical/blob/master/prj/pfc-edu/v4.0/pfc_edu%20manufacturing%20key.csv) (`NOTE: the orignal google sheet version is missing`)

### Additional Hardware
 - [Small components (MISSING DATA)]() you'll need (air pump, air stone, USB camera)
 
## Getting PFC_EDU Parts Manufactured
This list of manufacturers is meant to help OpenAg community members of all skill levels build a PFC_EDU. 
Add vendors you'd suggest to the [community list of manufacturers here (MISSING DATA)]().
 
You can build one on your own, or seek out your [local FabLab](https://www.fablabs.io/labs/map), [Makerspace](https://inventtolearn.com/resources-makerspaces-and-hackerspaces/), or contractors like those below 
(or in the [community list (MISSING DATA)]()) to help you get a chassis cut, a circuit board printed, or LED light panel created.
 
 - File(s) needed to get the [chassis made](https://github.com/OpenAgricultureFoundation/openag-mechanical/tree/master/prj/pfc-edu/v4.0).
 - File(s) needed to get the [reservoir made](https://github.com/OpenAgricultureFoundation/openag-mechanical/tree/master/prj/pfc-edu/v4.0/reservoir).
 - Files needed to get the [baseline CNS made](https://github.com/OpenAgricultureFoundation/openag-electrical/tree/master/prj/pfc-edu/v4.0), which includes circuit board, lights, fans, temp/humidity/CO2 sensors, & power supply. Does not include optional sensors.
 
### Mechanical Contract Manufacturers
 - [Plethora](https://www.plethora.com/)
 - [Xometry](https://www.xometry.com/)
 - [Protolabs](https://www.protolabs.com/)
 - [Cycle Start](http://cyclestart.com/)
 - [DSH Mould](https://www.dshmould.com/)
 - [Altec Plastics](http://altecplastics.com/)
 
### Electronic Assembly Houses
 - [7PCB](https://www.7pcb.com/)
 - [4PCB](https://www.4pcb.com/)
 - [Seeed Studio](https://www.seeedstudio.com/)
 
### Other Sources
 [Community's Manufacturer List (MISSING DATA)]()
 
*Note: Vendors listed here are simply suggestions of some manufacturers that may be helpful to the OpenAg community. 
Listing a vendor here doesn't suggest or imply the endorsement of these organizations, their products, or their 
services by MIT or the OpenAg community. As always, check your sources!*
 
## Licensing
 - License: GPL 3.0.
 - Documentation license: CC-BY-SA


