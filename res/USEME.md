# Calendar GUI

## Overview

Our application simulates a virtual calendar that lets the user create and use multiple calendars. The user also has the freedom to edit the calendar name and timezone. Also, this calendar GUI allows users to create single and recurring events based on their requirements. The user can add description to their events, tag it as private or public along with storing the necessary information like event name, location, start date and time and end date and time.

To use this application, the user must follow the below steps -

### Top Panel

- Firstly, going through the top panel, we have a default calendar called **default** that has a timezone - **America/New_York**. This is a dropdown that the user may use to change the calendar if they wish to. The user will be able to see this towards the left hand side of the top panel.

- To the extreme left of the dialog panel, the month and year are displayed. It has a forward **>** and a back **<** button to change the month and year.

- Right next to the calendar dropdown, there is a button to manage calendars. Click on the **+/✏ Manage Calendar** to create and edit calendars.

- Next to this there are two buttons, **Import** and **Export** for importing a CSV file(with events) into the selected calendar or to export events from the selected calendar to a CSV file respectively.

- Finally, towards the extreme right there is an edit events button **✏ events**  to edit multiple events together at once.

### Creating and Editing Calendars

- On clicking the **create calendar** button in the manage calendars dialog box, a new dialog box with a name and timezone text field opens.

- Here, the user can provide the calendars name and timezone and click the **create** button. The timezone should be in IANA format. 

- The user will receive a message pop up saying the calendars is created. The newly created calendar will get populated in the calendar dropdown in the top panel.

- Similarly, on clicking the **edit calendar** button in the manage calendars dialog box will take the user to the edit calendar dialog box. 

- This dialog box will have the current selected calendar name and the timezone displayed at the top along with two input fields below. One is a dropdown to select the calendar property that the user wishes to edit and the other is for entering the new value that they want to replace it with. 

- Once the change is done, the user will be notified with a test message and the calendar dropdown and timezone will be automatically updated in the top panel.


### View Events

- The user can view the list of all the events on a particular day by clicking on any day on the calendar. 

- This should open a dialog box with a list of all event's scheduled on that particular day.

- Next to each of these events there is a **view** and **edit** button.

- On clicking the view button, the user will be directed to a new dialog box displaying all the event details for that specific event.

- The details will include the event name, description, location, if it is a public or private event, start date time and end date time.

### Create Single and Recurring Events

- To create an event or events the user has to click on any day of the month, that would open a dialog box with a list of all events on that particular day along with a **create new event** button at the bottom.

- On clicking that, the dialog box will elongate and new input fields will be added to the dialog box.

- Firstly, there is a dropdown field at the top where the user can select what kind of event they want to create.

- Options include:
    - No Repeat
    - Repeat Weekdays
    - Repeat Weekends
    - Repeat Everyday
    - Custom Repeat

- "No Repeat" will create a **Single Event** and rest of the options would create **Recurring Events**.

#### Single Event

- With "No Repeat", the user will be asked to enter event name, description, location (description and location are optional values), start date time and end date time. 

- Also, there are two check boxes at the bottom, one to specify whether it is an all-day event(that would automatically fill the start date and end date time values) and one is to specify if it is a public or private event.

#### Recurring Event

- On choosing any other option than "No Repeat", the user will see two more options. 

- One is **Until** and the other is **Till Occurrences** (checkboxes). Until will make the event recur until a specific date and time. and occurrences will take in a number 'N' and make the event recur N times.

- Here -
    - Repeat Weekdays - event will recur only on weekdays(that is Monday, Tuesday, Wednesday, Thursday and Friday) until the specified end date or till the occurrences have finished.
    - Repeat Weekends - event will recur only on the week ends (that is Saturday and Sunday) until the specified end date or till the occurrences have finished.
    - Repeat Everyday - event will recur every day until the specified end date or till the occurrences have finished.
    - Custom Repeat - events will recur on the custom selection of days that user chooses.

- Finally, on clicking the **create** button at the bottom after filling in all the values will create the event is no conflicts are found. The user will be notified with a message pop up.

### Edit Single Event

- To edit a single event, the user can click on any day on the calendar and a dialog box with a list of all the events on that specific day will open and next to each event there is a view and edit button. 

- On clicking the **edit** button, the user will be directed to an edit event dialog box. 

- The current calendar will be displayed at the top with input text fields below. 

- Here, the user can enter the event name, select a property name(dropdown with valid property names) that they need to edit, the new property value they want to replace the old value with. 

- There will be input fields with the from date and time and end date and time that are automatically filled and uneditable.

- The editable properties are event name, description, ispublic flag, location, start date and time and end date and time. 

- On clicking the edit button in the edit event dialog box the event will be edited if no conflicts occur and the user will be notified via a message pop up.

### Editing Multiple Events

- To edit multiple events together, the user can click on the edit events button **✏ events** .

- This would open a dialog box with the current calendar displayed at the top and input text fields below. The user should enter the event name, select a property name(dropdown with valid property names) that they need to edit, the new property value they want to replace the old value with and finally the from date and time(this is optional). 

- Based on the user's input, all events with that name scheduled after or on the from date and time(will consider the from date and time only if the date is provided) will be modified with the new value. 

- The editable properties are event name, description, ispublic flag, and location. 

- Once, the event is modified the user will be notified with a success message.

### Exporting Events

- The user can click on the **Export** button on the top panel to export events from the selected calendar in to a CSV file.

- The user will be prompted to enter the path to the CSV file/file name.

- Here, the user can give just the name of the file if the file needs to be saved in the current project directory, or in the current directory of JAR Otherwise, the user should provide the absolute path for the file to be exported to that location.

-Our import and export functionality requires the file to be inside the src folder in the project for it to work with only the file name provided or the user will have to provide the absolute path to the file in both import and export.

- However, ensure that absolute path is always provided, as a good practice.

- On clicking **OK** the events in the calendar will be exported in to a CSV file and the user will be notified with a message.

### Importing Events

- The user can click on the **Import** button on the top panel to import events from a CSV file in to the selected calendar.

- The user will be prompted to enter the path to the CSV file/file name.

- Here, the user can give just the name of the file if the file is inside the src/main/utils of the project package. Otherwise, the user should provide the absolute path for the file so it can be imported from that location.

- However, ensure that absolute path is always provided, as a good practice.


- On clicking **OK** the events from the CSV file will be imported and the user will be notified with a message.
