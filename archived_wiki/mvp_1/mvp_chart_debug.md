---
layout: wiki_archive
---

#### MVP Chart Debugging

The charting program will have few problems. Occasionally you may not
see the data in the website, which may be due to the browser caching an
old image, and not displaying the most current. The program pulls data
from CouchDB, if you have good data there, things should work. If there
is no data (which should be there if the Validate.sh script successfully
ran), the chart will output with 'NO DATA' printed across it. The first
thing is to check that the database is up, and you have data. From the
command line, run the following:

> curl -g
> 'http:*localhost:5984/mvp\_sensor\_data/\_design/doc/\_view/attribute\_value?startkey=\["temperature"\]\&endkey=\["temperature",{}\]'
> If you have temperature data, this will bring it back. It fetches the
> design document and gets the attribute\_value view within it, passing
> the parameters for temperature data. Humidity data would look like:
> \>curl -g
> 'http:*localhost:5984/mvp\_sensor\_data/\_design/doc/\_view/attribute\_value?startkey=\["humidity"\]\&endkey=\["humidity",{}\]'

The next level of testing is to run the code (chartTemperature.py),
un-commenting the print statements so you can see output. For version
1.0

> python \~/MVP\_UI/python/chartTemperature.py

For version 3.0

> python \~/MVP/python/chartTemperature.py

The chart should be output to the web directory. This is a SVG graphic,
though it does not open properly with many graphic programs; double
clicking on it will often show a black page. You need to open it in a
browser to see the data.
