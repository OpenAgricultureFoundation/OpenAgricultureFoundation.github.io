---
layout: wiki_archive
---

## MVP 1.0

The MVP PFC (Minimal Viable Product) is a minimalist [Personal Food
Computer](../food_computer_2/getting_started.md) developed by OpenAg
Community members on the [OpenAg
Forum](http://forum.openag.media.mit.edu/t/mvp-community-development/1892) (*Note: Forum not available*),
in response to a call placed by MIT Open Agriculture Initiative's
Director Caleb Harper to build the "first truly community derived
device" for OpenAg.

![](/static/images/wiki/mvp/mvp.jpg)

For a quick overview, see the [promo
video](https://www.youtube.com/watch?v=yGGVXu1yMfQ&feature=youtu.be)

The OpenAg community's goal is to build something for around $300 (US)
that can produce significant research results with minimal investment
and skill. The MVP PFC allows for control and research around:

  - Nutrients
  - Light (photoperiod)
  - Temperature

The MVP PFC has the following main parts:

  - Enclosure
  - Brain
  - Reservoir
  - [User Interface](mvp_1.0_ui.md)

### Enclosure

The standard enclosure is a PVC and foil box.

### Brain

The brain is based around a Raspberry Pi and Python code, with cron used
as the scheduler. The latest code is located in
[Github](https://github.com/futureag).

Sensor data is currently logged to a flat file on the Pi's SD card, as
well as optionally being stored in CouchDB (on the Raspberry). By using
CouchDB, the data is available over the internet. Work is in process to
modify the existing PFC (Personal Food Computer) UI to access the MVP
data. While both the MVP and PFC use CouchDB, they use different
databases with different data structures.

Camera images are stored in a directory as jpg files.

Lighting is standardized on the GE Brit Stik LED (100w equiv, daylight).
We are still researching whether two or four are needed. A quick
experiment revealed that by removing the end covering and revealing the
LED, that the light intensity could be significantly increased.

There are two fans. One is always on for circulation, and the other is
thermostat controled for exhaust ventilation.

An [Adafruit
SI7021](https://learn.adafruit.com/adafruit-si7021-temperature-plus-humidity-sensor/overview)
temperature/humidity sensor and USB camera are the only standard
sensors; though there are open GPIO pins and two relays available for
future or custom expansion.

### Reservoir

The current system is hydroponic, the reservoir is a bus tub with an
air-pump and stone. Plants are started in rockwool and placed into net
pots in the reservior lid. All chemistry (EC and pH) are done manually.
There is active research in converting the MVP into an airoponic system.
While it will cost a bit more (for the pump) it will eliminate the need
for much of the chemistry.

### Resources

Check out our promo video for a quick summary of how to get started

1\. Assemble supplies Order parts from the [Bill of Materials
(BOM)](https://docs.google.com/spreadsheets/d/11uVNtVRwgM3ghLS6GWti2Bnrr1LLZmgzxPSaRIAi854/edit?usp=sharing)
Verify you have all required tools on second tab of BOM, if you are
missing any, order them.

2\. Machine parts into ready to assemble Prepared Parts: [Prepared Parts
Documentation](https://docs.google.com/presentation/d/1-RhLp98lgGOMHJ7TVwpK3idU7WbcJTbuMNNjlbJ5TME/edit?usp=sharing)

Be aware there are some inconsistencies between video and written
documentation. When in doubt: **Follow the written documentation as it
is updated to current BOM.**

3\. Build Enclosure: [Watch Enclosure Subassembly
Video](https://www.youtube.com/watch?v=SxPp5gJZcic) [Enclosure
Documentation](https://docs.google.com/presentation/d/1TVVPPh8ymDziJstBPThQpdcQynRyJOo_DGR2CHAkSU0/edit?usp=sharing)

4\. Build Top Panel or "Brain" assembly: [Watch "Brain" Subassembly
Video](https://www.youtube.com/watch?v=46w__wCbC6I) [Brain
Documentation](https://docs.google.com/presentation/d/1bXkGeTNTy66-_mO14JqDCGnvB5E5y3JXhQ38yVxRPP0/edit?usp=sharing)

5\. Build MVP Software Stack on SD card & Raspberry Pi: [Software
Documentation](https://docs.google.com/presentation/d/1YNNcF4PwlKjqAmt4XgMx4NBQcAw279qRtd0rp2uKJSg/edit?usp=sharing)
[Software Installation Guide on
GitHub](https://github.com/futureag/mvp#architecture)

6\. Complete Final Assembly [Final Assembly
Documentation](https://docs.google.com/presentation/d/1h53Dlnwfk4txx3D7bPjipJmu_femCNZAWq2onlkEO0c/edit?usp=sharing)

7\. Germinate seeds in Rockwool, balance your PH, and get growing\!
[Operational
Documentation](https://docs.google.com/presentation/d/1XIZdzpvIR4x0E80TgR2NLbtaRzQr0QnXLJ8R8A7IE9g/edit?usp=sharing)

8\. Get involved on the forums, show us your build and ask questions:
[Frequently Asked
Questions](https://docs.google.com/document/d/1NidizfnrUlMdpoob8cxGYLlP9Pt9y-u-Z_eImV1MtcI/edit)

9\. [Hacking the MVP](mvp_hacking.md) (Python code architecture)

### Additional Help

  - [code in Github](https://github.com/futureag)
  - [MVP Web Access](mvp_web_access.md)
  - [Testing and Debugging](mvp_debugging.md)
  - [Difficulty With MVP Hardware &
    Software](https://forum.openag.media.mit.edu/t/difficulty-with-mvp-system-test-si7021-failure/3104?u=webb.peter)
  - [MVP - Product Design
    Thread](http://forum.openag.media.mit.edu/t/mvp-product-design/1893)
  - [$300 Food Computer
    Thread](http://forum.openag.media.mit.edu/t/300-food-computer/2343)
  - [Networking MVPs to solve for Firewall
    Issues](http://forum.openag.media.mit.edu/t/networking-mvps-to-simplify-firewall-issues/2305?u=webb.peter)
  - [Troubleshooting MVP Build
    Thread](http://forum.openag.media.mit.edu/t/troubleshooting-mvp-build/2384)
  - [Akron Public
    Library](http://forum.openag.media.mit.edu/t/libraries-food-computers-plix-build-public-library-innovation-exchange-at-mit-media-lab/2895?u=webb.peter)
  - [Food Computer Greenhouse
    Integration](https://forum.openag.media.mit.edu/t/is-there-a-way-to-integrate-greenhouse-and-food-computers/3146?u=webb.peter)
  - [Brooklyn MVP at AgTechX using Open Agriculture Supply's
    pre-assembled "MVP Power
    Strip"](https://forum.openag.media.mit.edu/t/brooklyn-update-replicating-pfcs/2474)
  - [MVP UI
    Development](https://forum.openag.media.mit.edu/t/mvp-dashboard-in-nodered/3172)
    - Node-Red implementation as beta test for UI development.
  - [MVP Build in the
    Six](https://forum.openag.media.mit.edu/t/mvp-build-in-the-six/3366?u=webb.peter)
  - [Food Computer - Gipuzkoa Style - Several
    Designs](https://forum.openag.media.mit.edu/t/food-computer-gipuzkoa-style/3455?u=webb.peter)
  - [Fail at Buildscript -
    MVP](https://forum.openag.media.mit.edu/t/fail-at-buildscript-mvp/3671)
  - [My Experience Building the MVP Food
    Computer](https://forum.openag.media.mit.edu/t/my-experience-building-the-mvp-food-computer/4096)
  - [Error running MVP buildScript |
    mirror.stjschools.org](https://forum.openag.media.mit.edu/t/error-running-mvp-buildscript-mirror-stjschools-org/3825)
  - [Hacking the MVP UI for New
    Uses](https://forum.openag.media.mit.edu/t/mvp-ui-hacking-the-ui-for-new-uses/2105)
  - [Custom MVP Data Logging and
    Dashboard](https://forum.openag.media.mit.edu/t/custom-mvp-data-logging-and-dashboard/3764)
  - [Proposal: Collect MVP code & docs into one github
    repo](https://forum.openag.media.mit.edu/t/proposal-collect-mvp-code-docs-into-one-github-repo/4006)
  - [German MVP Build
    Instruction](https://forum.openag.media.mit.edu/t/german-mvp-build-instruction-deutsche-mvp-bauanleitung/3679)

### Alternate Builds and Materials

These builds are not the standard MVP, but alternative designs from the
community. Listings here are for information without any implied
recommendation or evaluation.

  - [MVP V1 Build
    Instructions](mvp_1.0_build_instructions.md)
    using a cardboard box and mylar liner
  - ["MVP Power
    Strip"](https://www.openagriculturesupply.com/product-page/open-agriculture-supply-mvp-food-computer-kit)
    - Open Agriculture Supply pre-assembled kit based on MVP.
  - [Yusuf's MVP PFC Outline](/contributors/yusuf/mvp_pfc).
  - [Food
    Rack](http://forum.openag.media.mit.edu/t/300-mvp-food-computer-variant-my-build/2687)
    - Another nice design. An expansion of the MVP into a
    multi-reservoir rack system.
  - [Alpha release of
    MVP](https://forum.openag.media.mit.edu/t/mvp-alpha-release-bill-of-materials/2019/3)
    Early release prior to finishing design.

### MVPs in Schools

  - [MARSfarm
    Curriculum.](https://forum.openag.media.mit.edu/t/growing-plants-in-space-marsfarm-curriculum/3056)
  - [Food Computers in
    Education](https://forum.openag.media.mit.edu/c/education)
  - [Classroom Resources on OpenAg EDU
    Wiki](../education.md)
