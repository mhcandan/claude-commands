Use AppleScript to find all Apple Notes modified today.

Run this command:
```
osascript -e 'tell application "Notes" to get name of every note whose modification date > (current date) - 1 * days'
```

Then summarize what I worked on based on the note titles returned.
