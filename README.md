# greminders2todoist

A simple script that helped me migrate from Google Inbox to Todoist.  Parse exports of Google Reminders (as in Google Inbox), especially the time/recurrence structure, and import into Todoist via the Todoist API.

# Setup and Usage

Install all requirements:

    pip install -e '.[test,dev]'

If you use PyCharm, make mypy's typeshed available to the IDE:

    bash setup-ide.bash

Register an app with Todoist, and create a client.json, using client.template.json as a template. Set the redirect
URL to http://localhost:3423.

Export your Google Reminders at https://takeout.google.com/ (select just Google Reminders to make it quick).

Run the script from the directory containing Reminders.html. Besides importing into Todoist, it will also produce an out.csv (comment out the Todoist code if you just want to see the CSV).

**By default, only reminders that are not already marked done, and are either recurrent or due in the future, are migrated.** If you want to tweak this logic, just edit the source.

Note that there are various limitations that you won't be able to import, due to limitations in how expressive Todoist's recurrence system is. For instance, "every N months on the first Monday" is something not supported (only N=1 works, i.e. "every month"). I tried to `assert` against encountering these, but review the code in `proc_date()` to be sure it's adequate for your needs.
