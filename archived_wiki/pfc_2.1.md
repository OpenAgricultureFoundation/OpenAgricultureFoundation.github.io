---
layout: wiki_archive
---


## Personal Food Computer 2.1

**\*Update 11 October 2018**: Please note
that the OpenAg Project paused research on these versions.

The OpenAg™ Personal Food Computer v2.1 is an evolution of
the [PFC v2.0](food_computer_2.md). This release includes a new light
panel and updated software.

The updated software is the latest release of the [openag_brain
v1.0.0](https://github.com/OpenAgricultureFoundation/openag_brain/releases). It
has several updates and many bug fixes.

For more details on testing done with the v2.1 updates, check out
[Reliability Test Grow log](/contributors/test_grows/basil_1.md) with
notes, problems, pictures and results.

Note:// The v2.1 LED light panel was custom-made by Tim (one of our
awesome OpenAg engineers) and uses red/white/blue [GE
LED's](http://www.gelighting.com/LightingWeb/na/solutions/sign-lighting/tetra-powermax.jsp).
Some users have hacked their PFC's to use an [off-the-shelf grow
light](http://forum.openag.media.mit.edu/t/minimalist-growing/1635/5)
panel. OpenAg is working on finding a light and supplier that fit system
requirements and can be purchased online as a single unit.//

Current Release
---------------

-   Download [BOM, CAD files and documentation on
    GitHub](https://github.com/OpenAgricultureFoundation/openag_pfc2/releases/tag/v2.0.0-beta)
-   Issues: If possible, **file issues with with the appropriate Github
    project**. If you don't know where to file the issue, [file it
    here](https://github.com/OpenAgricultureFoundation/openag_brain/issues).
-   License: [GPL
    3.0](https://www.gnu.org/licenses/quick-guide-gplv3.html).
-   Documentation license:
    [CC-BY-SA](https://creativecommons.org/licenses/by-sa/4.0/)
-   Code repositories:
    [github.com/OpenAgricultureFoundation](https://github.com/OpenAgricultureFoundation/)
    (all repositories).
-   [Build video!](https://youtu.be/Uf1FqjcPWsI?t=4)
-   [Software developers detailed setup
    instructions.](/contributors/rob.baynes/rpisetup)

## Release Notes


### Major Changes

-   The Arduino firmware codegen has been replaced by a version
    controlled src.ino script.
    [\#274](https://github.com/OpenAgricultureFoundation/openag_brain/pull/274)
-   rosserial has been replaced by a very basic bespoke serial protocol.
    [\#274](https://github.com/OpenAgricultureFoundation/openag_brain/pull/274)
-   openag\_python (previously a separate repo) has been deprecated and
    its functionality has been migrated over to
    openag\_brain/src/openag\_lib.
    [\#275](https://github.com/OpenAgricultureFoundation/openag_brain/pull/275)
-   Added support for openag\_brain\_box/fermentabot hardware.
    [\#278](https://github.com/OpenAgricultureFoundation/openag_brain/pull/278)
-   Fixed a long-term serial communications issue between the Raspberry
    Pi and Arduino
    [\#331](https://github.com/OpenAgricultureFoundation/openag_brain/issues/331)

### Minor Changes

-   All firmware modules no longer contain any blocking code.
-   Added an all\_vars view to the database. Also changed the csv
    exporter a bit.
    [\#288](https://github.com/OpenAgricultureFoundation/openag_brain/pull/288)
-   Decoupled the /desired value database persistence to a separate node
    instead of just the recipe handler.
-   Trace logging is enabled by simply doing `touch ~/TRACE`

### Bug fixes

-   The DoserPump firmware module doesn't crash the Arduino anymore.
-   The PID loop no longer adds to e\_i when the error is below the
    deadband which would cause runaway controllers.
-   [Many high-value issues
    fixed](https://github.com/OpenAgricultureFoundation/openag_brain/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aclosed%20label%3Ahigh-value%20).

### Downloads

-   [1.56 MB
    openag\_brain\_v1.0.0.tgz](https://github.com/OpenAgricultureFoundation/openag_brain/releases/download/v1.0.0/openag_brain_v1.0.0.tgz)

Resources
---------

-   [All the details about a PFC v2.1!](pfc_resources.md)
