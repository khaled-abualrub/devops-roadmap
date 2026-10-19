#bash areana

level 11 need to practice 

1-run:
#!/bin/bash

# Strict safety flags
set -euo pipefail

# Configuration
TARGET_DIR="/"          # Directory or partition to check
THRESHOLD=80            # Alert threshold percentage

echo "Checking disk usage for: $TARGET_DIR"

# 1. Get the usage percentage using 'df'
# df -P ensures portable output format across different Linux flavors
# awk 'NR==2 {print $5}' grabs the 5th column of the second row (the Use% column)
# tr -d '%' removes the percentage sign so we get a raw number
USAGE=$(df -P "$TARGET_DIR" | awk 'NR==2 {print $5}' | tr -d '%')

echo "Current disk usage: ${USAGE}% (Threshold: ${THRESHOLD}%)"

# 2. Compare usage against the threshold using integer math
if (( USAGE >= THRESHOLD )); then
    echo "[WARNING] Disk space is critically high! Usage is at ${USAGE}%."
    
    # In a real job, you would put your alert command here:
    # e.g., mail -s "Disk Alert" admin@company.com <<< "Usage is at ${USAGE}%"
    
else
    echo "[OK] Disk space is within safe limits."
fi


------------------------------------------------------------------


level 12 need to practice 

run:
#!/bin/bash

set -euo pipefail

CONFIG_FILE="app.conf"

# 1. Let's create a sample config file for testing purposes
cat << EOF > "$CONFIG_FILE"
# Application Configuration
HOST=127.0.0.1
PORT=3000
DB_NAME=users_db
DEBUG_MODE=true
EOF

echo "=== Reading configuration from $CONFIG_FILE ==="

# 2. The while read loop with IFS
while IFS='=' read -r key value; do
    
    # Skip empty lines or comment lines starting with '#'
    [[ -z "$key" || "$key" =~ ^# ]] && continue
    
    # Print or process the key-value pair
    echo "Found Config -> Key: [${key}] | Value: [${value}]"
    
    # Optional: You can actually export them or assign them as live variables in your script!
    # declare "$key"="$value"

done < "$CONFIG_FILE"

echo "=== Parsing Complete ==="

-----------------------------------------------------------------------

level 13 need to practice 


1-run:
#!/bin/bash

# Strict safety flags
set -euo pipefail

# Configuration
SOURCE_DIR="Arena"
BACKUP_DIR="Backups"
MAX_BACKUPS=5

# 1. Ensure backup directory exists
mkdir -p "$BACKUP_DIR"

# 2. Create a unique timestamp for the backup file name
TIMESTAMP=$(date +'%Y-%m-%d_%H-%M-%S')
BACKUP_NAME="backup_$TIMESTAMP.tar.gz"
BACKUP_PATH="$BACKUP_DIR/$BACKUP_NAME"

echo "=== Starting Backup ==="
echo "Backing up '$SOURCE_DIR' to '$BACKUP_PATH'..."

# 3. Create the compressed tar archive
# -c: create
# -z: compress with gzip
# -v: verbose (show files being added)
# -f: filename of the archive
tar -czvf "$BACKUP_PATH" "$SOURCE_DIR" > /dev/null

echo "Backup created successfully!"

echo "=== Managing Backup Rotation (Keeping last $MAX_BACKUPS) ==="

# 4. Rotation Logic:
# - ls -t: List backup files sorted by time (newest first)
# - tail -n +6: Skip the first 5 files (keep them), and select everything from file #6 onward (the old ones)
# - xargs rm -f: Delete those old files safely

# We use mapfile or a loop to safely handle files
cd "$BACKUP_DIR"

# Count how many backups we have
BACKUP_COUNT=$(ls -1 backup_*.tar.gz 2>/dev/null | wc -l)

if (( BACKUP_COUNT > MAX_BACKUPS )); then
    echo "Found $BACKUP_COUNT backups. Cleaning up old ones..."
    
    # List by time, skip the top N newest, and remove the rest
    ls -t backup_*.tar.gz | tail -n +$((MAX_BACKUPS + 1)) | xargs -r rm --
    
    echo "Cleanup complete. Only the last $MAX_BACKUPS backups remain."
else
    echo "Total backups: $BACKUP_COUNT. No cleanup needed yet."
fi

echo "=== Process Complete ==="


------------------------------------------------------------

level 14 need to practice

1-run:
#!/bin/bash

# Strict safety flags
set -euo pipefail

# --- Function 1: Check Disk Space ---
check_disk() {
    echo "==============================="
    echo "       DISK SPACE USAGE        "
    echo "==============================="
    df -h /
    echo ""
}

# --- Function 2: Show System Uptime ---
check_uptime() {
    echo "==============================="
    echo "         SYSTEM UPTIME         "
    echo "==============================="
    if uptime -p &>/dev/null; then
        uptime -p
    else
        uptime
    fi
    echo ""
}

# --- Function 3: List System Users ---
list_users() {
    echo "==============================="
    echo "         LOCAL USERS           "
    echo "==============================="
    # Extract usernames from /etc/passwd (first column separated by colon)
    cut -d: -f1 /etc/passwd | sort
    echo ""
}

# --- Function 4: Display Menu ---
show_menu() {
    echo "==============================="
    echo "      LINUX ADMIN TOOLKIT      "
    echo "==============================="
    echo "1) Check Disk Space"
    echo "2) Show System Uptime"
    echo "3) List System Users"
    echo "4) Exit"
    echo "==============================="
}

# --- Main Interactive Loop ---
main() {
    local choice
    while true; do
        show_menu
        read -rp "Enter your choice [1-4]: " choice
        echo ""

        case "$choice" in
            1) check_disk ;;
            2) check_uptime ;;
            3) list_users ;;
            4) 
               echo "Exiting tool. Have a great day!"
               exit 0 
               ;;
            *) 
               echo "[ERROR] Invalid choice. Please select a number between 1 and 4."
               echo ""
               ;;
        end case / case close)
        esac

        # Pause so the user can read the output before the menu redraws
        read -rp "Press Enter to continue..."
        echo ""
    done
}

# Execute main function
main "$@"


------------------------------------------------------------


level 15 need to practice

1-run:
#!/bin/bash

# Strict safety flags
set -euo pipefail

# Configuration constants
readonly TARGET_DIR="Arena"
readonly BACKUP_DIR="Backups"
readonly CONFIG_FILE="settings.conf"
readonly DISK_TARGET="/"
readonly DISK_THRESHOLD=80

# --- Function 1: Check Disk Space ---
check_disk_space() {
    echo "=== Disk Space Check ==="
    local usage
    usage=$(df -P "$DISK_TARGET" | awk 'NR==2 {print $5}' | tr -d '%')
    
    echo "Target Partition: $DISK_TARGET"
    echo "Current Usage: ${usage}% (Threshold: ${DISK_THRESHOLD}%)"
    
    if (( usage >= DISK_THRESHOLD )); then
        echo "[WARNING] Disk space usage is critically high!"
    else
        echo "[OK] Disk space is within safe limits."
    fi
    echo ""
}

# --- Function 2: Show System Uptime ---
show_system_uptime() {
    echo "=== System Uptime ==="
    # -p prints pretty uptime format on Linux
    if uptime -p &>/dev/null; then
        uptime -p
    else
        uptime
    fi
    echo ""
}

# --- Function 3: Backup Directory with Rotation (Keep last 3) ---
backup_arena() {
    echo "=== Backup Manager ==="
    
    if [[ ! -d "$TARGET_DIR" ]]; then
        echo "[ERROR] Source directory '$TARGET_DIR' does not exist."
        return 1
    }

    mkdir -p "$BACKUP_DIR"
    local timestamp
    timestamp=$(date +'%Y-%m-%d_%H-%M-%S')
    local backup_path="$BACKUP_DIR/backup_$timestamp.tar.gz"

    echo "Backing up '$TARGET_DIR' to '$backup_path'..."
    tar -czf "$backup_path" "$TARGET_DIR" 2>/dev/null
    echo "Backup created successfully."

    # Rotation: Keep last 3 backups
    local max_backups=3
    cd "$BACKUP_DIR"
    local backup_count
    backup_count=$(ls -1 backup_*.tar.gz 2>/dev/null | wc -l)

    if (( backup_count > max_backups )); then
        echo "Found $backup_count backups. Cleaning up old ones (keeping last $max_backups)..."
        ls -t backup_*.tar.gz | tail -n +$((max_backups + 1)) | xargs -r rm --
    fi
    cd - > /dev/null
    echo "Backup rotation complete."
    echo ""
}

# --- Function 4: Parse Configuration File ---
parse_config() {
    echo "=== Configuration Parser ==="
    
    # Create sample settings.conf if it doesn't exist
    if [[ ! -f "$CONFIG_FILE" ]]; then
        cat << EOF > "$CONFIG_FILE"
# Sample Settings
APP_ENV=production
TIMEOUT=30
MAX_CONNECTIONS=500
DEBUG=false
EOF
        echo "Created sample '$CONFIG_FILE'."
    fi

    echo "Reading values from '$CONFIG_FILE':"
    while IFS='=' read -r key value; do
        # Skip comments or empty lines
        [[ -z "$key" || "$key" =~ ^# ]] && continue
        echo "  [Key] $key ---> [Value] $value"
    done < "$CONFIG_FILE"
    echo ""
}

# --- Function 5: Display Menu ---
show_menu() {
    echo "==============================="
    echo "      DEVOPS UTILITY MENU      "
    echo "==============================="
    echo "1) Check Disk Space"
    echo "2) Show System Uptime"
    echo "3) Backup 'Arena' Directory (Keep last 3)"
    echo "4) Parse Configuration File"
    echo "5) Exit"
    echo "==============================="
}

# --- Main Program Loop ---
main() {
    local choice
    while true; do
        show_menu
        read -rp "Select an option [1-5]: " choice
        echo ""

        case "$choice" in
            1) check_disk_space ;;
            2) show_system_uptime ;;
            3) backup_arena ;;
            4) parse_config ;;
            5) 
               echo "Exiting tool. Goodbye!"
               exit 0 
               ;;
            *) 
               echo "[ERROR] Invalid option. Please choose between 1 and 5."
               echo ""
               ;;
        esac

        echo "Press Enter to return to the menu..."
        read -r
    done
}

# Run the main function
main "$@"
