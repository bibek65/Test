# 1. Basics

Copy your  `/etc/passwd`  file to  `/tmp`  and write a script to display the following:

-   Full contents of the file sorted in ascending order (display the whole file)
-   Total number of lines in the file
-   Total number of characters in the file
-   All usernames containing the letter  `s`
-   All usernames starting from  `r`

Copying /etc/passwd file to /tmp

    cp /etc/passwd /tmp/passwd_copy

**Bash Script**

```
#!/bin/bash

# Full contents of the file sorted in ascending order
echo "Full contents of the file sorted in ascending order:"
sort /tmp/passwd_copy

# Total number of lines in the file
echo -e "\nTotal number of lines in the file:"
wc -l /tmp/passwd_copy | awk '{print $1}'

# Total number of characters in the file
echo -e "\nTotal number of characters in the file:"
wc -m /tmp/passwd_copy | awk '{print $1}'

# All usernames containing the letter 's'
echo -e "\nUsernames containing the letter 's':"
cut -d: -f1 /etc/passwd | grep 's'

# All usernames starting from 'r'
echo -e "\nUsernames starting from 'r':"
awk -F':' '$1 ~ /^r/ {print $1}' /tmp/passwd_copy

```


# 2. Naive Parser

Given the following CSV file, write a Bash script to find if the total number of delimeters in the file is correct.

```
		id|first_letter|last_full|age
		0|S|Dangol|24
		1|P|Koirala|17
		2|S|Dotel|18
		3|N|Shresth|19
		4|A|Joshi|22|
```

**Bash Script**

  
This script aims to ensure consistency in the number of delimiters across all lines in a CSV file.

The first line as the header have 3 delimiters.

The total expected delimiters should be 3 times the number of lines.

In the given example with 6 lines, the expected total is 18 delimiters.

However, the script found 19 delimiters.

So it displayed **“Error: The total number of delimiters is incorrect.”**

```
#!/bin/bash

# Define the filename
filename="temp.csv"

# Function to count delimiters in each line
count_delimiters() {
    local line="$1"
    local delimiter="|"
    local count=$(grep -o "$delimiter" <<< "$line" | wc -l)
    echo "$count"
}

# Main script
total_delimiters=0
no_of_lines=$(wc -l < "$filename")
delimiter=$(grep -o "|" <<< "$(head -n 1 "$filename")" | wc -l) #Counting delimiters in first line

while IFS= read -r line; do
    # Count delimiters in the line
    delimiter_count=$(count_delimiters "$line")
    total_delimiters=$((total_delimiters + delimiter_count))
done < "$filename"

correct_delimiters=$((delimiter * no_of_lines))

if [ "$total_delimiters" -eq "$correct_delimiters" ]; then
    echo "The total number of delimiters is correct."
else
    echo "Error: The total number of delimiters is incorrect."
fi
```
**Output**

![Screenshot](materials/1.png)


## 3. Cron

Write a cron job that runs every hour. It should:

-   Fetch the HTML response from  `https://www.example.com`
-   Log the output inside this directory  `/var/log/bash_assignment/`
-   Compress all previous logs as a ZIP archive
-   Keep only 5 most-recent archives and delete all other archives

Cron Job that runs every hour is

	0 * * * * /bin/bash /tmp/script.sh

**Bash Script**

```
#!/bin/bash

# Set the directory for log files
log_directory="/var/log/bash_assignment"

# Fetch HTML response and log
timestamp=$(date +"%Y%m%d_%H%M%S")
curl -s https://www.example.com > "$log_directory/response_$timestamp.html"

# Compress previous logs as a ZIP archive
cd "$log_directory"

# Remove previous tar.gz file if it exists
if [ -e "all_logs_archive.tar.gz" ]; then
    rm -f "all_logs_archive.tar.gz"
fi

# Create a new tar.gz archive
tar -czf "all_logs_archive.tar.gz" *.html

# Keep only 5 most-recent archives and delete others
ls -t response_*.html | tail -n +6 | xargs rm -f

```
**Output**

![Screenshot](materials/2.png)



