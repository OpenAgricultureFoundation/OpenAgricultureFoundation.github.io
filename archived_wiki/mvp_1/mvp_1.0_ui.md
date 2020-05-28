---
layout: wiki_archive
---

### MVP 1.0 User Interface

This is a work in process. Details will be added over the next several
days, and code will be made available on Github. Specific documentation
on the code will be in the <https://github.com/futureag> README.md and
within the code itself.

The UI is a composite of various small parts that come together to
create a local, but web accessible interface to temperature and humidity
charts, and the latest image from the camera.

While it took a bit to pull all of this together, each part is small and
simple. I consider this code less of a finished product (though it is a
MVP complete deliverable) that a starting point for to hack and expand.
You should need little knowledge of Python and shell scripts to get
started.

#### Assumptions

  - Camera images are stored in \~/Documents/OpenAg-MVP/webcam
  - Sensor data is stored in CouchDB, in a mvp\_sensor\_data database
    (record layout described elsewhere)
  - You can do some port forwarding on your router to make the site
    accessible.

#### Parts

  - [CouchDB views](mvp_1.0_couchdb_views.md) that give query access to the
    data
  - A bash shell script the moves the latest picture to the web
    directory, and generates SVG files of the data charts. This script
    is invoked once an hour by cron.
  - A static index.html file that displays the chart and pictures in
    separate tabs. 
  - A shell script that calls the Python HTTP Server code
  - A minimalist Python web server (SimpleHTTPServer) configured to
    display SVG images.
  - [Port forwarding](mvp_web_access.md) enable on your router.
