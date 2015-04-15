## Events

The calendar extension allows you to manage events and display them in a
calendar or event list on the website. Unlike articles that are associated with
a particular page, events are organized in calendars, which allows you to easily
group, categorize or export them.


### Calendars

Calendars are used to group and/or categorize events. Each calendar can relate
to a certain language or a particular topic.


### Front end modules

Front end modules are used to display events on the website. They can be
configured with the "Modules" module in the back end and have to be added to an
article or page layout to actually show up on the website. The calendar
extension includes four front end modules:

<table>
<tr>
  <th>Module</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Calendar</td>
  <td>mod_calendar</td>
  <td>Adds a calendar to the page.</td>
</tr>
<tr>
  <td>Event reader</td>
  <td>mod_eventreader</td>
  <td>Shows the details of an event.</td>
</tr>
<tr>
  <td>Event list</td>
  <td>mod_eventlist</td>
  <td>Adds a list of events to the page.</td>
</tr>
<tr>
  <td>Event list menu</td>
  <td>mod_eventmenu</td>
  <td>Generates a navigation menu to browse the event list.</td>
</tr>

</table>


### Permalinks

Each event has a unique URL (permalink) that can be used to reference it:

```
http://www.example.com/event-reader/events/final-exams.html
```

The above URL requests the event "final-exams" via the page "events". Remember
that Contao is a page-based CMS, so if the page "events" did not exist or if it
did not include the event reader module, the event would not be displayed.
