# Read Me

System notifications such as downtime notices or information about system disruptions are stored here.

JSON in notifications is automatically validated in a pre-commit hook to ensure we don't break anything when manually creating JSON notifications. Malformed JSON won't be able to be committed to the repo. 

Once you have the repo set up locally, run NPM install before committing, otherwise the pre-commit hook won't run.

## How to post a new notification

- If you want a 2nd pair of eyes on it create a new branch `git checkout -b <branch-name>` and publish it.
- In the notifications.json file, first delete old expired notifications if any, to minimize clutter
- Then add your new notification
- Start with a notification that is only visible to admins `[4]`
- If you want review, commit, push and open a PR
- If you are going live immediately, commit and push to `main`
- Log out of Codon and log back in, make sure the notification looks good
- Change role visibility if necessary

## What a notification looks like:

```javascript
{
  "id":4 // Unique identifier for the notification, can be anything as long as it not used by any other active notification
  "notificationStart": "2024-11-07T16:00:00-04:00", // Start time of the notification (ISO 8601 format)
  "notificationEnd": "2024-11-07T20:20:00-04:00",   // End time of the notification (ISO 8601 format)
  "downtimeStart": "2024-11-07T18:10:00-04:00",     // Start time of planned downtime (ISO 8601 format)
  "downtimeDuration": { 
    "minutes": 20                 // Duration of downtime in minutes
  },
  "message": "Notification 4",            // The content/message of the notification
  "showToRoles": []                       // Array of roles that can view this notification. Any empty array indicates the message should be displayed to all roles
}
```
Roles:
- 1	= Instructor
- 2	= Student
- 3	= TeachingAssistant (not in use)
- 4	= Admin
