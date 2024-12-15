---
layout: page
title: Application
description: Discussion of a work schedule implementation.
permalink: /app/
---
A work schedule application has been built to demonstrate fundamental capabilities of the library.  The user interface is implemented in JavaFX 11 and database persistency is provided by JPA 2.2 (Java Persistence API) with FXML descriptors in the shift_orm.xml file. Hibernate is the JPA implementation for a supported relational database. The editor allows new schedules to be created and saved to the database as well as updated and deleted.

This screen capture shows shift instances for the month of June, 2017 with the DNO schedule selected.

<img src="../resources/images/ShiftInstances.png" alt="Shift Instances" style="width:100%; display: block; margin-left: auto; margin-right: auto;">

To display shift instances, the steps are to:
- Select the schedule in the drop-down, e.g. DNO Plan.  
- Choose the beginning date from the picker and enter the beginning time of day (hour:minute)
- Choose the ending date from the picker and enter the ending time of day (hour:minute)
- Click the "Show Shifts" button.  The shift instances starting in each day will be displayed in the table along with the total working and non-working time for each such shift instance. 

The "Editor ..." button launches the editor. This screen capture shows the work schedule editor.

<img src="../resources/images/ShiftEditor.png" alt="Shift Editor" style="width:100%; display: block; margin-left: auto; margin-right: auto;">

To create a work schedule, click the "New" button and enter a name and description.

Select the Shifts tab.  Click New and enter the shift information.  Click Add to create a shift.  To update a shift, select it in the table, edit the information and click Update.  Click Remove to delete it. For the Rotations, Teams and Non-working Periods, the steps are similar.

Click the "Save" button.  The new work schedule will appear in the list view on the left. To edit a work schedule, select it in the list view.  It's properties will be displayed on the right.  Change properties as required, then click the "Save" button.

Clicking the Refresh button will refresh the state of the work schedule that is selected in the list view.


To delete a work schedule, select it in the list view then click the "Delete" button.

The screen capture below shows the work schedule editor with the Rotations tab selected.  The rotation duration is displayed in the table.

<img src="../resources/images/RotationEditor.png" alt="Rotation Editor" style="width:100%; display: block; margin-left: auto; margin-right: auto;">

The screen capture below shows the work schedule editor with the Teams tab selected.  The average hours worked per week is displayed in the table.

<img src="../resources/images/TeamEditor.png" alt="Team Editor" style="width:100%; display: block; margin-left: auto; margin-right: auto;">

The screen capture below shows the work schedule editor with the Non-working Periods tab selected.

<img src="../resources/images/NonWorkingEditor.png" alt="Non Working Editor" style="width:100%; display: block; margin-left: auto; margin-right: auto;">

<a href="index.html">Return to top</a>