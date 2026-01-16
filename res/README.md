

# Introduction
This project supports both a command-line abd GUI based calendar application that allows users to create, edit, query, and export events. It supports single and recurring events, conflict management, and CSV export for compatibility with Google Calendar and CSV import in GUI. The application runs in interactive, headless and in a GUI mode.

Users can run the application in one of the following modes:

- Interactive Mode: Enter commands one at a time through the terminal.

- Headless Mode: Execute a batch of commands from an input file.

- GUI Mode: Use a user-friendly graphical interface to manage calendars and events, including the ability to import events from a CSV file (available only in GUI mode). The GUI mode can be run through the JAR commands with the JAR file.

### How to use the application?


##### This is for command-line interaction

Step 1: Run the main CalendarApp method and then in the terminal after the application prompts you to pass a valid mode, pass the mode that you desire as args as follows:

For interactive mode:
>--mode interactive

For Headless Mode:
>--mode headless commands.txt

- Interactive mode features a command line interface where the user can execute various functions, till the user passes exit or a runtime error occurs.
- Headless mode takes in a file as input and parses command in the file till it encounters an exit.
- Headless mode exists the application if it encounters any errors while executing the commands or if the commands are invalid.
- Whereas in interactive mode the error will be shown to the user and the user will be allowed to enter more commands.
- The GUI mode can be run through the JAR commands with the JAR file.

### Assumptions
Assumptions in our project:

1. Conflicts are never allowed while creating and editing events.
2. You cannot edit start and date time for multiple events, as this is prone for conflict inconsistencies. If you want to, you may edit start date time for a single event by specifying its start and end date time
3. Recurring events don’t allow for editing of start and date time values as this would break chains.


### Using the JAR file

Please download our Assignment6 zip file submission where you can find the .jar file.
After doing this you can now run these scripts in the terminal.

This will run in headless mode.

> java -jar Assignment6.jar --mode headless validcommands.txt

This will run in interactive mode.

> java -jar Assignment6.jar --mode interactive

This will run in GUI mode.

> java -jar Assignment6.jar

#  A list of changes to the design of our program

### Model

Our model is untouched from Assignment 5 and does not have any changes for Assignment 6.

#### Assignment 4

- Our Model previously had 6 files. They are as follows :
    - AbstractEvent.java
    - Calendar.java
    - ICalendar.java
    - ExportToCSV.java
    - RecurringEvent.java
    - SingleEvent.java
- RecurringEvent was extending SingleEvent.
- SingleEvent was extending AbstractEvent.
- Calendar was implementing ICalendar interface.

#### Assignment 5

- Currently, our Model has 8 files. They are as follows :
    - AbstractEvent.java
    - Calendar.java
    - ICalendar.java
    - ConflictException.java
    - RecurringEvent.java
    - SingleEvent.java
    - CalendarCollection.java
    - ICalendarCollection.java
- ICalendarCollection interface represents a store for a collection of calendars of type ICalendar.
- CalendarCollection implements the ICalendarCollection and this class represents a store for a collection of calendars of type ICalendar, that implements the ICalendarCollection interface.
- ExportToCSV was moved to the controller as that is best practice to read/write files through the controller rather than the model.
- Currently, the RecurringEvent and SingleEvent both are extending only the AbstractEvent. We made this change to ensure proper abstraction and proper code maintainability moving forward.
- We added a new ConflictException class to throw exceptions for conflicts between events. This enables us to handle the exceptions more gracefully.
- We added additional interfaces to make sure our code is scalable and maintainable.

### View

#### Assignment 4
- Previously we had a single class for our view that is CalendarOutputView which handled all the output logic.

#### Assignment 5
- Now we now have two public classes in our view folder.
- One is the ICalendarOutputView interface and the other is the CalendarOutputView class that implements the ICalendarOutputView interface.
- We made this change so that our code base can be more scalable and flexible for future adaptations or new feature additions.
- Adding the interface now makes out View code more reliable and standardized.

#### Assignment 6
- We have added two new files in the View for our Assignment 6. They are as follows -
    - ICalendarGUI.java
    - CalendarGUI.java

- ICalendarGUI interface is being implemented by the CalendarGUI. CalendarGUI is our main view for the GUI mode. It interacts with the controller for each operation.
- All the controller calls or requests are made in the addFeatures(IGUIFeatures controller) method through the addActionListners(). The view does not have direct access to the model and interacts with the controller to perform all calendar operations.
- The View takes instructions from the controller for all operations. New dialogs or other components are invoked through the controller.

### Controller

#### Assignment 4

- Our controller previously had 6 files. They are as follows :
    - AbstractInputMode.java
    - InteractiveMode.java
    - HeadlessMode.java
    - CalendarController.java
    - QueryParser.java
    - InvalidCommandException.java
- InteractiveMode and HeadlessMode both extend the AbstractInputMode class.
- CalendarController acted like the main controller of our application.
- QueryParser was a helper class that parser all the user commands.

#### Assignment 5

- For assignment 5, we had 9 files. They are as follows :
    - AbstractInputMode.java
    - InteractiveMode.java
    - HeadlessMode.java
    - CalendarController.java
    - ICalendarController.java
    - IExport.java
    - ExportToCSV.java
    - QueryParser.java
    - InvalidCommandException.java
- We retained all our old files and build upon it based on a few changes that we thought were a must.
- Our Query parser was bulky and was handling logic that we thought would be better moved to the model.
- This lighted the load on the queryParser.
- We moved the ExportToCSV file from the model to the controller as reading or writing into/from a file should be handled in the controller.
- For this we added an interface IExport.java so that in the future more implementations can be added if required without changing the existing code.
- The ExportToCSV class is implementing the IExport class.
- We also ICalendarController class that the CalendarController implements for the same reason as stated before. This would make our code scalable and helps us avoid editing any existing logic.
- Apart from these the res of the classes remain the same.
- Also, we noticed coupling in our controller where multiple model classes were being called in the same controller class which was not best practice. Hence, we decided to restructure our logic inside the class. Now we only call utmost one model class in any of our controller classes.


#### Assignment 6

No files were removed from from the controller since assignment 5. We have added two new files to support the GUI mode. They are as follows :
    - IGUIFeatures.java
    - GUIController.java

- We have added a new interface IGUIFeatures that is implemented by the GUIController which interacts with the View and the model.
- Our code is properly structured to follow the MVC architecture. 
- Only the GUIController interacts with the GUI View and all the methods invoked in the View are through the controller. Our View is dumb and takes all instructions from the controller. 
- The controller invokes all methods in the view. That is, opening new dialog boxes and any data updation request goes through the controller to the model.

# Features

All the below mentioned features are supported in all the three modes. However, with GUI no commands are passed. But these features are available and made easy to use for the users in the GUI application.

### Create/Edit/Use Calendar

This application now allows users to create, edit and use a calendar of their choice. The user has to first use a calendar before creating/edit/printing/exporting events. Basically, all event related operations cannot be performed until the user creates a calendar and passes a use command to use that calendar.
-To create a calendar the user as to provide the name of the calendar and the timezone in IANA format.
-The use can also edit the calendar's name and timezone one at a time.
-And to the use a calendar the user has to pass a simple use calendar command with the name.

The create/edit/use commands are as follows:

> create calendar --name calName --timezone area/location

> edit calendar --name name-of-calendar --property property-name new-property-value

> use calendar --name name-of-calendar

### Copy Events

Additionally, this calendar application also allows the user to copy events from one calendar to another calendar.
THe user can copy single event, multiple events on a specific day or multiple events between a range of days.
They should also pass the target calendar name and the new datetime for the copied events in the target calendar.

The copy commands are as follows:

To copy a single event
>copy event eventName on dateStringTtimeString --target calendarName to dateStringTtimeString

To copy all events on a specific date
>copy events on dateString --target calendarName to dateString

To copy all events between a range
>copy events between dateString and dateString --target calendarName to dateString

### Event Creation

Create single events with start day, optional start time, end day and end time, description, location, and privacy settings to set the event public or otherwise.
AutoDecline is now deprecated and no events that are conflicting will be created.

Create all-day events by omitting the end date and time.
Create recurring events (e.g., "every Monday, Wednesday, Friday for 5 times" or "until a given date").
A recurring event repeats on specific days of a week (as indicated by the user) for a specific number of occurrences or until a specific end date and time. A single event in the recurring series can only span one day, that is, it must start and finish on the same day.

An event is created using the create command as follows:

>create event --autoDecline eventName from dateStringTtimeString to dateStringTtimeString repeats weekdays until dateStringTtimeString

>create event --autoDecline eventName on dateStringTtimeString

>create event eventName on dateString repeats weekdays for N times

>create event eventName on dateString repeats weekdays until dateString

### Conflict Handling

If an event conflicts with an existing one:

- With --autoDecline enabled → The event is not created.
- Without --autoDecline → Both events are preserved.
- Two recurring events will always arise a conflict.

### Event Editing

Modify a specific event, a series from a given date, or all instances of a recurring event.
Change properties like event name, location, visibility, description, start datetime and end datetime

>edit event property eventName from dateStringTtimeString to dateStringTtimeString with NewPropertyValue

>edit events property eventName from dateStringTtimeString with NewPropertyValue

>edit events property eventName NewPropertyValue

### Querying Events

The following features are supported:

-List all events on a specific date.
-Find events within a date range.

This can be done using:

>print events on dateString

>print events from dateStringTtimeString to dateStringTtimeString

A user can check if busy or otherwise too, with the show command.

>show status on dateStringTtimeString

### Export to CSV

-Export calendar events to a CSV file that can be imported into Google Calendar.
As follows:

>export cal events.csv.

### Import CSV to Calendar (only available in GUI)

-Import calendar events from a CSV file in to a selected calendar in the Calendar GUI application.


# Division of work

Assignment 4

- Tasks were evenly divided between us, with the implementation of single events done by Geethanjali and recurring done by Ashwin.

- The controller and query parser were jointly and collaboratively worked on.

- The interactive view was done by Geethanjali while the headless was done by Ashwin.

- Export functionality was also done by Ashwin.

Assignment 5

- The controller and view logic was handled by Geethanjali.

- The model logic and functionality was handled by Ashwin.

- Planning and getting the structure of the application together was a common effort.

- Tests for the controller and view was handled my Geethanjali.

- Tests for the model were handles my Ashwin.

- Similarly, creation of resources was also split among us.

Assignment 6

- Both of us worked on the calendar and the View.

- Little to no changes were made in the Models.

- Tasks were evenly divided between us, with the implementation of edit events/event, create/edit calendars and showevents was done by Geethanjali and create events, import and export was done by Ashwin.

- Controller tests and mocks were written by Ashwin.

- Planning and getting the structure of the application together was a common effort.


### All of the aforementioned features are fully functional in all of the three modes except for copy events. Copy events is not supported in GUI mode.

# In Summary,

- We have created a class called Calendar Collection.java that stores all calendars in an List.

- In our assignment 4 controller implementation, we noticed our controller was highly coupled with our model. Now, the controller interacts with just one object of model belonging to class calendar collection. We store a string of the current calendar used. We may now access previous methods of the calendar using the calendar collection class by chaining inputs.

- In our model we have made Facade methods called Facade create, facade edit and facade print. The controller interacts with the model for create edit and print operations using these facade methods. In create it parses and finds keywords and sends them to the model, the model now checks for keywords and then further fine tune the methods for createEvent(we have implemented method overloading so it checks for the matching parameters and calls the relevant one), editEvent and queryEvents methods.

- Previously in assignment 4, edit start date operations didn’t check for conflicts, we have added that functionality for assignment 5.

- The RecurringEvent extends AbstractEvent, instead of previously extending

- We have moved ExportToCSV to controller, as IO operations should be handled in the model.

- We have adjusted our code in such a way that we didn't have to make any changes in the model or re-write any existing code from Assignment 5. 

- We fully developed the GUI View (CalendarGUI) and its interface (ICalendarGUI).

- Created the GUI Controller (GUIController) and feature interface (IGUIFeatures) to link the GUI with the underlying model.

- The CalendarGUI class has an addFeatures(IGUIFeatures controller) method that sets the controller to IGUIFeatures and handles all controller-related calls. It manages all the ActionListeners for button clicks and calendar changes, and it calls the appropriate methods in the controller. The controller has a setView() method that sets the view to ICalendarGUI. The controller is responsible for invoking all the relevant methods in the view to display dialog boxes and interact with the model to make changes to the data.

- Enabled CSV import functionality in GUI mode to allow users to load events visually.

- Our import and export functionality requires the file to be inside the src or the utils folder in the project for it to work with only the file name provided or the user will have to provide the absolute path to the file in both import and export.

- Ensured a clean separation between view and controller—GUI only interacts with the model via the controller.



#### NOTE: We couldn’t achieve 100% mutation coverage as many lines were structurally unreachable due to our code design. These lines couldn’t be executed under any valid input or test scenario.

