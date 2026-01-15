Search my Apple Notes for a keyword.

Ask me what to search for, then run:
osascript -e 'tell application "Notes"
  set matches to (notes whose name contains "[KEYWORD]" or body contains "[KEYWORD]")
  set output to ""
  repeat with n in matches
    set output to output & name of n & "\n"
  end repeat
  return output
end tell'
