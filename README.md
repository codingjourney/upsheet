# upsheet

uploads a simple plain-text timesheet into Jira as a bunch of worklog entries. Given a _timesheet.txt_ containing

    20130130
      1945-2015 UPSH-22 cleaning up the code
    20130131
      0530-0600 UPSH-21 writing a README
      0600-0630 UPSH-22 setting up a GitHub repository

when you say

    $ upsheet timesheet.txt

it creates one worklog entry for issue UPSH-21 and two for UPSH-22.

### Configuration

upsheet is a simple Python script with all configuration defined as constants at the beginning:

    # Configuration
    URL  = "http://localhost:8080/rest/api/latest/issue/%s%s"
    USER = "admin"
    PASS = "" # if empty, user will be prompted for password

If you need to upload timesheets to different Jira instances you'll have to make multiple copies of the script, adjusting the settings as needed.

### Rationale

I work as a contractor on a project where Jira worklogs are used as basis for invoicing so it's pretty important to keep them up to date. Jira is a fine piece of software overall but firing up the worklog entry form each time I'm switching tasks is a pain. Appending a line to a file is much easier so I ended up keeping a plain-text timesheet and updating Jira once a day.

That was the plan, anyway. I ended up spoon-feeding Jira for a solid hour at the end of each month. Not fun. I always had a hunch that Jira probably had a REST API and when I got around to reading the docs it didn't look that hard. The present script is the result of a few months of gradual tweaking.

### Future

Some colleagues prefer a timesheet file format where only the start time of an activity is logged:

    20130131
      0830 PROJ-3998 writing Selenium tests for the assignment page
      1200 lunch
      1230 PROJ-3995 fixing the assignment page
      1800 out for the day

You can see the trade-off: breaks in activity have to be mentioned explicitly. upsheet is not friends with such files but I can imagine a version that would be. It could even auto-detect which format is being used and adapt.

Supporting other time-tracking systems besides Jira is also an option but I'm afraid it would pollute what is now a sharply focused tool.

More realistic objectives are to be found in the issue tracker. 
