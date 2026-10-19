#bash areana

level 6
Mission: Write a script that accepts a filename as an argument and prints the number of lines in that file. If no filename is provided, display a message saying 'No file provided'.


1-run:
#!/bin/bash


file_name() {

   local file="$1"
   if [[ -z "$file" ]]; then
   echo "no file provided"
   

   elif [[ -e "$file" ]]; then

   file=$(wc -l "$file")
   echo "the number of lines are: $file"

   else

   echo "the file does not exist please provide an existant one"
   fi 


}


file_name warrior.txt


------------------------------------------------------------------


level 7
Mission: Write a script that sorts all .txt files in a directory by their size, from smallest to largest, and displays the sorted list.


1-run:
#!/bin/bash


sorting_directory() {

   local directory="$1"

   if [[ -d "$directory" ]]; then

   echo "the sorted files from smallest to largest are: $sorting"

   ls -Sr "$directory"/*.txt
   
   else 

   echo "your directory does not exist "
   fi
   
}

sorting_directory Battlefield

---------------------------------------------------------------------


level 8
Mission: Create a script that searches for a specific word or phrase across all .log files in a directory and outputs the names of the files that contain the word or phrase.

1-run:

#!/bin/bash


sorting_directory() {

   local directory="$1"

   if [[ -d "$directory" ]]; then

   for file in "$directory"/*.log; do
   grep -l "hello" "$file"
   done
   
   else 

   echo "your directory does not exist "
   fi
   
}

sorting_directory Battlefield


-------------------------------------------------------


level 9 need to practice it
Mission: Write a script that monitors a directory for any changes (file creation, modification, or deletion) and logs the changes with a timestamp.

1-run:
#!/bin/bash

DIRECTORY="Arena"
LOG_FILE="change_log.txt"

# 1. Ensure the directory exists
if [ ! -d "$DIRECTORY" ]; then
    echo "Error: Directory '$DIRECTORY' does not exist."
    exit 1
fi

echo "Monitoring directory '$DIRECTORY' on Linux... Press [CTRL+C] to stop."

# 2. Monitor using inotifywait
# -m : monitor continuously
# -r : recursive (watches subdirectories)
# -e : events to watch (create, modify, delete)
inotifywait -m -r -e create,modify,delete \
  --format '%T [%e] %w%f' \
  --timefmt '%Y-%m-%d %H:%M:%S' \
  "$DIRECTORY" | while read -r timestamp event filepath; do

    # Format event into clean human-readable text
    case "$event" in
        *CREATE*)  ACTION="File created" ;;
        *MODIFY*)  ACTION="File modified" ;;
        *DELETE*)  ACTION="File deleted" ;;
        *)         ACTION="File changed ($event)" ;;
    esac

    # Build the log line
    LOG_LINE="[$timestamp] $ACTION: $filepath"

    # Print to screen and append to log file
    echo "$LOG_LINE"
    echo "$LOG_LINE" >> "$LOG_FILE"

done

------------------------------------------------------------------


level 10 need to practice it 

1-run:
#!/bin/bash

# Exit immediately if a command fails
set -euo pipefail

TARGET_DIR="Arena_Boss"
ARCHIVE_DIR="Victory_Archive"

# 1. Create the directories
mkdir -p "$TARGET_DIR" "$ARCHIVE_DIR"

echo "=== Creating and populating files ==="

# Words to randomly throw into the lines
WORDS=("Battle" "Defeat" "Combat" "Victory" "Glory" "Challenge" "Shield" "Sword")

# 2. Loop to create file1.txt through file5.txt
for i in {1..5}; do
    FILE="$TARGET_DIR/file$i.txt"
    
    # 3. Generate a random number of lines between 10 and 20
    # $RANDOM % 11 gives 0 to 10. Adding 10 makes it 10 to 20.
    NUM_LINES=$(( (RANDOM % 11) + 10 ))
    
    # Empty/create the file
    > "$FILE"
    
    for ((line=1; line<=NUM_LINES; line++)); do
        # Pick a random word from our WORDS list
        RANDOM_WORD=${WORDS[$((RANDOM % ${#WORDS[@]}))]}
        
        # Write a line with some random text length to vary file sizes
        echo "Line $line: Boss fight log entry with status $RANDOM_WORD" >> "$FILE"
    done
    
    echo "Created $FILE with $NUM_LINES lines."
done

echo ""
echo "=== 4. Sorting files by size (Largest to Smallest) ==="
# -l for detailed view, -S to sort by size
ls -lhS "$TARGET_DIR"

echo ""
echo "=== 5. Checking for 'Victory' and archiving ==="
for FILE in "$TARGET_DIR"/*.txt; do
    # Check if the file exists (handles edge cases)
    [[ -f "$FILE" ]] || continue
    
    # grep -q runs quietly without printing the match to stdout
    if grep -q "Victory" "$FILE"; then
        echo "Found 'Victory' in $FILE -> Moving to $ARCHIVE_DIR/"
        mv "$FILE" "$ARCHIVE_DIR/"
    else
        echo "No victory in $FILE -> Staying in $TARGET_DIR/"
    fi
done

echo ""
echo "=== Process Complete ==="










