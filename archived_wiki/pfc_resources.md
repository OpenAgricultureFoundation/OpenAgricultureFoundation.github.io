How to Build and Run a PFCv2.x\*
================================

\*Update March 2018: Please note that MIT OpenAg at the Media Lab has
paused research on this version, and while these build resources remain
available here and on our GitHub, MIT OpenAg can't support community
members' individual builds of this versions. If you\'re building this
version (or your own modification of this version!), [let us
know](https://docs.google.com/forms/d/e/1FAIpQLSd6UDIJKbYq-LOPOTddIMNqpUrH4OZX3i3BH2kfzo63JwJXTA/viewform)!
[For more details, see this community forum
post](https://forum.openag.media.mit.edu/t/update-from-openag-please-read/3171).

Getting Started
---------------

  - [PFC 2.0 Build Video](https://youtu.be/Uf1FqjcPWsI)

Hardware
--------

  * [CAD files, build guide, BOM, DFX files, drawings](https://github.com/OpenAgricultureFoundation/openag_pfc2)

Software (\"openag\_brain\")
----------------------------

### Core system:

  * [High Level PFC Architecture](food_computer_2/architecture.md)
  * [[openag_brain:]]: the program that runs on the single-board computer ([[:Raspberry Pi]])
  * [Step-by-step install instructions][openag_brain:installing: | ]
    * [[openag_brain:installing:installing_globally | developer install script]] will install the core system on a Raspberry Pi. This is recommended for development only.

### Database (the \"Open Phenome Library\")

  * Data is stored in [CouchDB](http://couchdb.com/). See [CouchDB documentation](http://docs.couchdb.org/en/2.0.0/) for more.
  * The [[openag_brain:database]] page has documentation for the Food Computer database schemas.

### Firmware

  * Arduino firmware for sensors and actuators. [[:openag_brain]] automatically handles fetching, compiling and flashing firmware for your given sensor configuration.

### Web User Interface (UI)

  * [[openag_ui:]]: a web-based UI for controlling the Personal Food Computer that can be served from the single-board computer.

### Hotlinks

  * [[openag_brain:CLI | openag_brain CLI (command line interface)]]
  * [[/openag_ui/ | User Interface (openag_ui)]]
  * [[openag_brain:api| API]]
     * [[openag_brain:api:0.0.1]]
  * [[openag_brain:0.1.0:Fixtures]]
  * [[openag_brain:Firmware Modules]]
  * [[openag_brain: Database]] 
  * [[Recipe: | Climate Recipes]]
  * [[:raspberry pi | Working with Raspberry Pi]]
  * [[docker| Working with Docker]]
  * [[openag_brain:ROS | Working with ROS]]
  * [[:Contributing]]
     * [Setting up a development environment](food_computer_2/development.md)
  * [[:Troubleshooting]]
