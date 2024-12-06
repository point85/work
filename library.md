---
layout: page
title: Library
permalink: /lib/
---
<h3>DNO Schedule</h3>
The DNO schedule discussed in the Introduction is defined in Java as follows:
String description = "This is a fast rotation plan that uses 3 teams and two 12-hr shifts to provide 24/7 coverage. "
    + "Each team rotates through the following sequence every three days: 1 day shift, 1 night shift, and 1 day off.";
WorkSchedule schedule = new WorkSchedule("DNO Plan", description);
// Day shift, starts at 07:00 for 12 hours
Shift day = schedule.createShift("Day", "Day shift", LocalTime.of(7, 0, 0), Duration.ofHours(12));
// Night shift, starts at 19:00 for 12 hours
Shift night = schedule.createShift("Night", "Night shift", LocalTime.of(19, 0, 0), Duration.ofHours(12));
// rotation
Rotation rotation = new Rotation("DNO", "DNO");
rotation.addSegment(day, 1, 0);
rotation.addSegment(night, 1, 1);
schedule.createTeam("Team 1", "First team", rotation, referenceDate);
schedule.createTeam("Team 2", "Second team", rotation, referenceDate.minusDays(1));
schedule.createTeam("Team 3", "Third team", rotation, referenceDate.minusDays(2));

To obtain the working time over three days starting at 07:00, the following methods are called:
LocalDateTime from = LocalDateTime.of(referenceDate, LocalTime.of(7, 0, 0));
Duration duration = schedule.calculateWorkingTime(from, from.plusDays(3));


To obtain the shift instances for a date, the following method is called:
List<ShiftInstance> instances = schedule.getShiftInstancesForDay(LocalDate.of(2017, 3, 1)); 


To print a work schedule, call the toString() method.  For example:
Schedule: DNO Plan (This is a fast rotation plan that uses 3 teams and two 12-hr shifts to provide 24/7 coverage. Each team rotates through the following sequence every three days: 1 day shift, 1 night shift, and 1 day off.)
Rotation duration: PT216H, Scheduled working time: PT72H
Shifts: 
  (1) Day (Day shift), Start : 07:00 (PT12H), End : 19:00
  (2) Night (Night shift), Start : 19:00 (PT12H), End : 07:00
Teams: 
  (1) Team 1 (First team), Rotation start: 2016-10-31, Rotation periods: [Day (on), Night (on), (off) ], Rotation duration: PT72H, Days in rotation: 3, Scheduled working time: PT24H, Percentage worked: 33.33%, Average hours worked per week: PT56H
  (2) Team 2 (Second team), Rotation start: 2016-10-30, Rotation periods: [Day (on), Night (on),(off) ], Rotation duration: PT72H, Days in rotation: 3, Scheduled working time: PT24H, Percentage worked: 33.33%, Average hours worked per week: PT56H
  (3) Team 3 (Third team), Rotation start: 2016-10-29, Rotation periods: [Day (on), Night (on), (off) ], Rotation duration: PT72H, Days in rotation: 3, Scheduled working time: PT24H, Percentage worked: 33.33%, Average hours worked per week: PT56H
Total team coverage: 100%


To print shift instances between two dates, the following method is called:
schedule.printShiftInstances(LocalDate.of(2016, 10, 31), LocalDate.of(2016, 11, 3)));

with output:
Working shifts
[1] Day: 2016-10-31
  (1) Team: Team 1, Shift: Day, Start : 2016-10-31T07:00, End : 2016-10-31T19:00
  (2) Team: Team 2, Shift: Night, Start : 2016-10-31T19:00, End : 2016-11-01T07:00
[2] Day: 2016-11-01
  (1) Team: Team 3, Shift: Day, Start : 2016-11-01T07:00, End : 2016-11-01T19:00
  (2) Team: Team 1, Shift: Night, Start : 2016-11-01T19:00, End : 2016-11-02T07:00
[3] Day: 2016-11-02
  (1) Team: Team 2, Shift: Day, Start : 2016-11-02T07:00, End : 2016-11-02T19:00
  (2) Team: Team 3, Shift: Night, Start : 2016-11-02T19:00, End : 2016-11-03T07:00
[4] Day: 2016-11-03
  (1) Team: Team 1, Shift: Day, Start : 2016-11-03T07:00, End : 2016-11-03T19:00
  (2) Team: Team 2, Shift: Night, Start : 2016-11-03T19:00, End : 2016-11-04T07:00

24/7 Manufacturing Plant Schedule

For a second example, the 24/7 schedule below has two rotations for four teams in two shifts.  It is used by manufacturing companies.
WorkSchedule schedule = new WorkSchedule("Manufacturing Company - four twelves",
  "Four 12 hour alternating day/night shifts");
// day shift, start at 07:00 for 12 hours
Shift day = schedule.createShift("Day", "Day shift", LocalTime.of(7, 0, 0), Duration.ofHours(12));
// night shift, start at 19:00 for 12 hours
Shift night = schedule.createShift("Night", "Night shift", LocalTime.of(19, 0, 0), Duration.ofHours(12));
// 7 days ON, 7 OFF
Rotation dayRotation = new Rotation("Day", "Day");
dayRotation.addSegment(day, 7, 7);
// 7 nights ON, 7 OFF
Rotation nightRotation = new Rotation("Night", "Night");
nightRotation.addSegment(night, 7, 7);
schedule.createTeam("A", "A day shift", dayRotation, LocalDate.of(2014, 1, 2));
schedule.createTeam("B", "B night shift", nightRotation, LocalDate.of(2014, 1, 2));
schedule.createTeam("C", "C day shift", dayRotation, LocalDate.of(2014, 1, 9));
schedule.createTeam("D", "D night shift", nightRotation, LocalDate.of(2014, 1, 9));


When printed out for a week of shift instances, the output is:
Schedule: Manufacturing Company - four twelves (Four 12 hour alternating day/night shifts)
Rotation duration: PT1344H, Scheduled working time: PT336H
Shifts: 
  (1) Day (Day shift), Start : 07:00 (PT12H), End : 19:00
  (2) Night (Night shift), Start : 19:00 (PT12H), End : 07:00
Teams: 
  (1) A (A day shift), Rotation start: 2014-01-02, Rotation periods: [Day (on), Day (on), Day (on), Day (on), Day (on), Day (on), Day (on), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT336H, Days in rotation: 14, Scheduled working time: PT84H, Percentage worked: 25%, Average hours worked per week: PT42H
  (2) B (B night shift), Rotation start: 2014-01-02, Rotation periods: [Night (on), Night (on), Night (on), Night (on), Night (on), Night (on), Night (on), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT336H, Days in rotation: 14, Scheduled working time: PT84H, Percentage worked: 25%, Average hours worked per week: PT42H
  (3) C (C day shift), Rotation start: 2014-01-09, Rotation periods: [Day (on), Day (on), Day (on), Day (on), Day (on), Day (on), Day (on), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT336H, Days in rotation: 14, Scheduled working time: PT84H, Percentage worked: 25%, Average hours worked per week: PT42H
  (4) D (D night shift), Rotation start: 2014-01-09, Rotation periods: [Night (on), Night (on), Night (on), Night (on), Night (on), Night (on), Night (on), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT336H, Days in rotation: 14, Scheduled working time: PT84H, Percentage worked: 25%, Average hours worked per week: PT42H
Total team coverage: 100%
Working shifts
[1] Day: 2014-01-09
  (1) Team: C, Shift: Day, Start : 2014-01-09T07:00, End : 2014-01-09T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-09T19:00, End : 2014-01-10T07:00
[2] Day: 2014-01-10
  (1) Team: C, Shift: Day, Start : 2014-01-10T07:00, End : 2014-01-10T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-10T19:00, End : 2014-01-11T07:00
[3] Day: 2014-01-11
  (1) Team: C, Shift: Day, Start : 2014-01-11T07:00, End : 2014-01-11T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-11T19:00, End : 2014-01-12T07:00
[4] Day: 2014-01-12
  (1) Team: C, Shift: Day, Start : 2014-01-12T07:00, End : 2014-01-12T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-12T19:00, End : 2014-01-13T07:00
[5] Day: 2014-01-13
  (1) Team: C, Shift: Day, Start : 2014-01-13T07:00, End : 2014-01-13T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-13T19:00, End : 2014-01-14T07:00
[6] Day: 2014-01-14
  (1) Team: C, Shift: Day, Start : 2014-01-14T07:00, End : 2014-01-14T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-14T19:00, End : 2014-01-15T07:00
[7] Day: 2014-01-15
  (1) Team: C, Shift: Day, Start : 2014-01-15T07:00, End : 2014-01-15T19:00
  (2) Team: D, Shift: Night, Start : 2014-01-15T19:00, End : 2014-01-16T07:00


Firefighter Schedule

For a third example, the work schedule below with one 24 hour shift over an 18 day rotation for three platoons is used by Kern County California firefighters.
WorkSchedule schedule = new WorkSchedule("Kern Co.", "Three 24 hour alternating shifts");
// shift, start 07:00 for 24 hours
Shift shift = schedule.createShift("24 Hour", "24 hour shift", LocalTime.of(7, 0, 0), Duration.ofHours(24));
// 2 days ON, 2 OFF, 2 ON, 2 OFF, 2 ON, 8 OFF
Rotation rotation = new Rotation("24 Hour", "2 days ON, 2 OFF, 2 ON, 2 OFF, 2 ON, 8 OFF");
rotation.addSegment(shift, 2, 2);
rotation.addSegment(shift, 2, 2);
rotation.addSegment(shift, 2, 8);
Team platoon1 = schedule.createTeam("Red", "A Shift", rotation, LocalDate.of(2017, 1, 8));
Team platoon2 = schedule.createTeam("Black", "B Shift", rotation, LocalDate.of(2017, 2, 1));
Team platoon3 = schedule.createTeam("Green", "C Shift", rotation, LocalDate.of(2017, 1, 2));


When printed out for a week of shift instances, the output is:
Schedule: Kern Co. (Three 24 hour alternating shifts)
Rotation duration: PT1296H, Scheduled working time: PT432H
Shifts: 
  (1) 24 Hour (24 hour shift), Start : 07:00 (PT24H), End : 07:00
Teams: 
  (1) Red (A Shift), Rotation start: 2017-01-08, Rotation periods: [24 Hour (on), 24 Hour (on), (off), (off), 24 Hour (on), 24 Hour (on), (off), (off), 24 Hour (on), 24 Hour (on), (off), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT432H, Days in rotation: 18, Scheduled working time: PT144H, Percentage worked: 33.33%, Average hours worked per week: PT56H
  (2) Black (B Shift), Rotation start: 2017-02-01, Rotation periods: [24 Hour (on), 24 Hour (on), (off), (off), 24 Hour (on), 24 Hour (on), (off), (off), 24 Hour (on), 24 Hour (on), (off), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT432H, Days in rotation: 18, Scheduled working time: PT144H, Percentage worked: 33.33%, Average hours worked per week: PT56H
  (3) Green (C Shift), Rotation start: 2017-01-02, Rotation periods: [24 Hour (on), 24 Hour (on), (off), (off), 24 Hour (on), 24 Hour (on), (off), (off), 24 Hour (on), 24 Hour (on), (off), (off), (off), (off), (off), (off), (off), (off) ], Rotation duration: PT432H, Days in rotation: 18, Scheduled working time: PT144H, Percentage worked: 33.33%, Average hours worked per week: PT56H
Total team coverage: 100%
Working shifts
[1] Day: 2017-02-01
  (1) Team: Black, Shift: 24 Hour, Start : 2017-02-01T07:00, End : 2017-02-02T07:00
[2] Day: 2017-02-02
  (1) Team: Black, Shift: 24 Hour, Start : 2017-02-02T07:00, End : 2017-02-03T07:00
[3] Day: 2017-02-03
  (1) Team: Red, Shift: 24 Hour, Start : 2017-02-03T07:00, End : 2017-02-04T07:00
[4] Day: 2017-02-04
  (1) Team: Red, Shift: 24 Hour, Start : 2017-02-04T07:00, End : 2017-02-05T07:00
[5] Day: 2017-02-05
  (1) Team: Black, Shift: 24 Hour, Start : 2017-02-05T07:00, End : 2017-02-06T07:00
[6] Day: 2017-02-06
  (1) Team: Black, Shift: 24 Hour, Start : 2017-02-06T07:00, End : 2017-02-07T07:00
[7] Day: 2017-02-07
  (1) Team: Green, Shift: 24 Hour, Start : 2017-02-07T07:00, End : 2017-02-08T07:00