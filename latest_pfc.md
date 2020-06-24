---
layout: bootstrap
---

## Personal Food Computer resources
Here you'll find descriptions of the various Github repositories that were used to create both the hardware and software
for the last version of the PFC-EDU that was in development at the end of 2019.

### Hardware
The OpenAg hardware consists of electrical and mechanical assets. The electrical assets are housed in the [OpenAg-electric](https://github.com/OpenAgricultureFoundation/openag-electrical)
repositories under `prj/pfc-edu/v4.0` with the current design files and BOM.  Whereas, the latest mechanical cut files are housed in the [OpenAg-mechanical](https://github.com/OpenAgricultureFoundation/openag-mechanical) repository. 
Any updates on contract manufacturers information will be posted here in the future, if applicable.  

### Software
Software can be divided into two parts, the **Device Software**, which is the software the controls the physical PFC, along with 
support software for management of wifi connections and using [Balenia.io](https://www.balena.io/) to manage a fleet of machines.

Then there is the **Cloud Software** which was run up on [Google Cloud](https://cloud.google.com/) for hosting 
web based interfaces, collection of data and images from the machines, and even export of that data for data-scientists. 
There is a [small project](https://github.com/OpenAgricultureFoundation/self_hosted_backend) that adapts some of these 
pieces and replaces others so that someone can self-host the backend without needing a large cloud
infrastructure like Google. You'll find descriptions and pointers to the relevant GitHub repositories below.

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
There is a [local services](https://github.com/OpenAgricultureFoundation/self_hosted_backend) project that runs a lightweight 
backend with [docker-compose](https://docs.docker.com/compose/) which enables collection of data one a small local machine. 

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
The OpenAg [Data API](https://github.com/OpenAgricultureFoundation/Data_API) provides access to the backend services via 
a Python [Flask](https://flask.palletsprojects.com/en/1.1.x/) based Web API. It relies on the [cloud_common](https://github.com/OpenAgricultureFoundation/cloud_common) project, as well as [Auth0](https://auth0.com/) for initial
log in. 

##### EDU_UI
The OpenAg [Education User Interface](https://github.com/OpenAgricultureFoundation/EDU_UI) is [reactjs](https://reactjs.org/)
web application for controlling PFC-EDU bots from 'the cloud'. It was designed to run alongside the [Data_API]() on Google's 
Cloud Platform. Logging into the UI utilizes the [Auth0](https://auth0.com/) OpenID Connect service, but could be transitioned to another OIDC provider.
Once logged in, the EDU_UI and Data_API use a home brew token system, because the effort to transition the API over to OIDC/OAuth
was never completed.