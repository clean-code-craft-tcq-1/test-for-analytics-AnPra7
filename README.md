# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file.
2. Access to the library functions for finding maximum and minimum, counting breaches etc.
3. Access to the time stamp( date and time from the system).
4. Technique for creating the PDF.
5. Access to the storage server for storing PDF.
6. Sending the Notification through email or text.
7. Defining thresholds

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This will ensure the pdf creation from the csv file
Counting the breaches       | Yes           | This is part of the software being developed which will ensure the battery health
Detecting trends            | Yes           | This is part of the software being developed and tend to help improve performance 
Notification utility        | Yes           | This is being developed and should be tested if functioning correctly since other APIs involved too

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "Threshold Crossed" to the PDF whenever exceeds the maximum value or recedes the minimum value
4. Write the Count of breaches in the pdf with the time stamps whenever breach happens.
5. Write the Count of breaches after the 7 days count
6. Show the trend of the battery after the 7 days battery telemetrics
7. Write "No CSV file found" when the proper file format not present or no file present.
8. Write "Server not acessible" when the server for storing pdf is not reachable
9. Write "Notified" when the Notification is sent successfully
10. Write "Failure in Notifying" when unable to send notification or negative feedback received for Notification.
11. Write "PDF Generated" when the pdf is created from the CSV file.
12. Write " Trend Recorded" with date and time  when the reading was continuously increasing for 30 minutes
13. Write "Pdf generated" after 7 day data is provided.
14. Write "Storage Error" depending on the feedback from the server if storage fails due to any issue.


(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | PDF file     | Notification via email/sms  | Fake the email notification
Report inaccessible server | Server address | feedback from server api  | Fake the server
Find minimum and maximum   | csv file     | min/max value               | None - it's a pure function
Detect trend               | csv file     | Trend with date and time    | None - it's a pure function
Write to PDF               | csv file     | PDF file                    | Mock pdf generation
