# Maintenance Schedules

Maintenance Schedules are a collection of preventative maintenance tasks that need to happen once or on a recurring basis.  A typical example is the periodic maintenance performed on an aircraft every few hundred hours or annually.

### Schedule Tolerance

In certain circumstances, a maintenance schedule can have a tolerance where the maintenance activity can be performed within a range of time and still meet regulatory requirements.  These tolerances fall into three categories:

* **Fixed** - the use of a tolerance is ignored and the date/usage of the next scheduled maintenance action is based on the previously scheduled date/usage.  In this case, if the operation is scheduled for every 200 hours with a 10 hour tolerance and the last was completed at 205 hours, the next would remain scheduled for 400 hours.
* **Cummulative** - the date/usage of the next next scheduled maintenance action is based on the last release to service.  Here, if the schedule was for 200 hours and the last was completed at 205 hours, the next would be scheduled for 405 hours. If the last was completed early at 195 hours, the next would be scheduled at 395 hours.
* **Not Extended** - in this case, maintenance is scheduled from the eariler of the last operation or the last scheduled date/usage.  In other words, if the mainenance is performed early, the next schedule will be early. If the tolerance is late, the next schedule will not be extended. Here, if the schedule was for 200 hours and the last was completed at 205 hours, the next would be scheduled for 400 hours. If the last was completed early at 195 hours, the next would be scheduled at 395 hours.





