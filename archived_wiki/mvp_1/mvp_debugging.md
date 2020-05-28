---
layout: wiki_archive
---

## Testing and Debugging

The MVP comes with a validation script which exercises the main
components of the code. It can be run at any time to confirm that things
are set up correctly and running properly. If you encounter problems
(things stop working), running the validation script is always a good
first step in finding the problem. In MVP 1.0 it can be tested via:

> bash \~/OpenAg-MVP/setup/Validate.sh

In MVP 3.0 it can be tested via:

> bash \~/MVP/setup/Validate.sh

If all is correct, no errors will be seen. If there is an error, you
will see it displayed in RED. The script runs starting with low level
issues and works its way up through complexity. Always fix the first
error encountered and re-run the script. Fixing low level issues will
often take care of things higher up, and low level issues are almost
guaranteed to create other problems (ie. if a sensor is not working, you
will not log data or produce a data chart). The validation script gives
little output. If you have an error, run the referenced script of code
individually from the command line. For scripts:

> bash \<path to command\>\<command.sh\>

For python code:

> python \<path to code\>\<code.py\>

You should also be able to click (or double click) on a python file to
open in in the IDE and run it from there. These will give you the error
details, which should point you toward what needs to be fixed. Though
the code is not robust (having a lot of error handling), because it is
simple and has been running for a while, you should encounter few (if
any) actual code problems. Most problems have to do with the setup and
configuration, often the problems are with typing errors in cron (which
is not in the validation script).

#### Test Steps

##### Directory Tests

The first step is to make sure the main directories are in place, that
you didn't copy things from Github to the wrong location. If you
encounter an error here, re-copy the Github download to the correct
location. See the <https://github.com/futureag> for correct deployment.

##### CouchDB

This part checks that CouchDB is set up correctly, running, and has the
proper database and view file. If the first test fails, it means the
CouchDB is not running. Either it was not installed properly, or you
need to reboot your system to get it running. The second test looks for
the database where sensor data is stored. If it is missing, run the
script to build it (see the README.md) The third test checks for the
view script, this is needed to generate the charts. If it is missing,
run the script to build it (see the README.md)

##### Variable Persistence

There are a couple of variables stored to help track the state of the
MVP. 1.0 used the Python 'shelf' library, while 3.0 stores them in
CouchDB. If this step fails, you likely did not load the variables (for
1.0 you may have a Python version conflict).

##### Sensor Testing

These tests perform low level reads of the sensors. If you encounter
problems here, it is likely a wiring problem.

##### Data Logger

This runs the code that logs sensor data to CouchDB. If you have gotten
this far, the sensors are working, and CouchDB is up; you are unlikely
to see any issues here. This step assures there is something in the
database for the chart to report.

##### Actuator Test

When this test runs, you will likely hear your relay clicking, lights
flashing and the fan going off and on. Software issues are unlikely,
though this may show up some wiring problems. The USB camera will also
be checked, by trying to take a picture.

##### Build Website

Since it is assumed that there is data in CouchDB, and you have a new
picture, this step runs

> render.py

Which will move the latest picture to the UI web directory and build the
charts. Again, if you got to this point, there is little that can go
wrong. Open your brower and check things to see what you have.

> <http://localhost:8000>

For more detailed testing of the charting, see [here](mvp_chart_debug.md).

##### Logs and Output

It is always good to check these for errors or problems. For problems
with cron, check the log:

> /var/log/cron.log

Ignore "No MTA installed". This is saying that you do not have email set
up to send cron output messages.

For Server logs: In MVP 1.0 the log is at:

> \~/MVP\_UI/server.log

In MVP 3.0 the log is at:

> \~/MVP/logs/server.log
