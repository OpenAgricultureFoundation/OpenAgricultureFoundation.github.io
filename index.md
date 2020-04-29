---
layout: bootstrap
---
# Open Agriculture Foundation
Welcome to the OpenAgriculture Foundation. Here you will find information about the various software
and hardware solutions that were created by OpenAg.

## Data Sets
Several sets of data were collected with OpenAg devices and published on GitHub.

### Basil Flavor Data
The Basil Flavor data contained in [flavor-data](https://github.com/OpenAgricultureFoundation/flavor-data) was collected
for the [Flavor-cyber-agriculture: Optimization of plant metabolites in an open-source control environment through surrogate modeling](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0213918)
paper. The goal of the paper was to show that applying machine learning to controlled environment growing could increase 
production of compounds in a plant. In this case optimizing the environment to produce more flavor compounds in basil.

The repository contains the measurements of volatile molecules as collected, measured, and identified by 
[headspace-solid phase microextraction-gas chromatography-mass spectrometry (HS-SPME-GC-MS, or GC-MS for short)](http://www.chromatographyonline.com/headspace-solid-phase-microextraction-coupled-gas-chromatography-mass-spectrometry-characterization).

### Cooper-Hewitt Data
From May 2019 through January 2020, 3 different PFC machines were set up in the [Cooper-Hewitt Museum](https://www.cooperhewitt.org/).
While network connectivity was an issue for two of the machines (due to conditions at the museum), at least one of the PFC-EDU
machines reported back data for nearly the entire time in the museum. The [Cooper_Hewitt_PFC_Data](https://github.com/OpenAgricultureFoundation/Cooper_Hewitt_PFC_Data)
repository contains all the data collected with some visualizations of the data from that one machine. While in the museum, 
the PFC was growing basil, while running a single light recipe. At times the plants were replaced as they grew to large/old, and the machine was 
cleaned a few times. (You can see the timing of the cleanings in PH and EC measurements)

### Tomato Experiment
While developing software for the PFC-EDUs one team member decided to grow [Tiny Tim dwarf tomato plants](https://www.seedsnow.com/products/tomato-tiny-tim) 
in three PFC-EDU machines, with different conditions (A control, one with basil in the same machine, and one that had no photo-rest period, but
used blue (no-ir) light for the night phase. All the data was recorded for the 3 or so months, along with harvest data. 
You can find this data in the [Tomato_Experiment](https://github.com/OpenAgricultureFoundation/Tomato_Experiment) repository.

## Personal Food Computer resources
The resources available here are mostly for the Personal Food Computer 3 or later (also known as the PFC-EDU).

### Software
#### Device Software
The latest version of the software was developed for the version 4 of the machine that ran off 
a [Raspberry Pi](https://www.raspberrypi.org/) computer.

##### openag-device-software
The [openag-device-software repository](https://github.com/OpenAgricultureFoundation/openag-device-software) contains 
the [Django](https://www.djangoproject.com/) based software that runs on the physical PFC-EDU device. This software communicates
with the hardware over `I2C` as well as with a backend that used to run on [Google's Cloud Platform (GCP)](https://cloud.google.com/).

OpenAg's instance of the cloud platform has been shutdown, but modifications to the code to allow running locally are currently being made.
(Information will be updated as soon as it is available.)

##### openag-brain-balena
While the device software can be run directly on a Raspberry Pi 3, you can manage deployment and upgrading of one
or more devices via [Balena.io](https://www.balena.io/). Balena provides an infrastructure to deploy and manage 
[Docker](https://www.docker.com/) based 'applications' on smaller embedded hardware such as the Raspberry Pi. 

The [openag-brain-balena repsoitory](https://github.com/OpenAgricultureFoundation/openag-brain-balena) is a ready to go
project that depends on the `openag-device-software` to power PFC machines.

##### python-wifi-connect
[python-wifi-connect](https://github.com/OpenAgricultureFoundation/python-wifi-connect) is a python implementation of 
[Balena's wifi-connect](https://github.com/balena-io/wifi-connect) project. It is used by [openag-brain-balena](https://github.com/OpenAgricultureFoundation/openag-brain-balena)
to configure the wifi on a Raspberry Pi via a captive portal on which can be accessed by a browser. The OpenAg implementation
also allowed for presenting the user with a 'device registration code' which could be used to associate the device with a user
account on the cloud software.

#### Cloud Software
There are several pieces of software that were designed to run in the cloud.

##### cloud_common
The [cloud_common repository](https://github.com/OpenAgricultureFoundation/cloud_common) collected several cloud specific 
functions and interfaces that are used by many of the cloud based software projects. These include things like tying into
[Google  BigQuery](https://cloud.google.com/bigquery) and [Google Datastore](https://cloud.google.com/datastore), etc. The 'cloud_common' 
repository is used as a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) in the other projects.

##### firebase-cloud-functions
A [Google Firebase Cloud Function](https://firebase.google.com/docs/functions) is located in [firebase-cloud-functions](https://github.com/OpenAgricultureFoundation/firebase-cloud-functions)
This function is  part of registering the device with [Google's PubSub](https://cloud.google.com/pubsub/)

##### mqtt-service
Any OpenAg device that is communicating with the backend (Google, or soon, locally) uses the [mqtt](http://mqtt.org/) 
messaging protocol. On the cloud/server side, the [mqtt-service project](https://github.com/OpenAgricultureFoundation/mqtt-service) 
listens to mqtt topics to receive sensor data from the device, and sends commands down to the device 
(such as starting an environmental recipe). The [cloud_common](https://github.com/OpenAgricultureFoundation/cloud_common)
repository is used when running on Google's cloud platform.

##### Data_API
TODO: fill in Data API

##### EDU_UI
TODO: fill in EDU UI

### Hardware
TBD