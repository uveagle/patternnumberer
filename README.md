# patternnumberer written by UV-EAGLE
# a simple bash script that matches a string in your text file and numbers it sequentially throughout the file. For example numbering the first occurence of the string "quality" to quality_1, the second occurence of the string "quality" to quality_2, etc. 

#!/bin/bash
count=0
old_string="quality"
# Define the string to add as a prefix to the numbers.
prefix="quality_"
# Use sed to replace the old string with a unique placeholder and save the output to a temporary file.
sed "s/$old_string/##PLACEHOLDER##/g" "./nano.txt" > "./temp.txt"
# Use awk to replace the placeholder with a sequential number with the specified prefix and save the output to the output file.
awk -v prefix="$prefix" '{while(match($0, /##PLACEHOLDER##/)) {$0 = substr($0, 1, RSTART-1) prefix (++count) substr($0, RSTART+RLENGTH)}; print}' "temp.txt" > "./mugatu.txt"
# Remove the temporary file.
rm "temp.txt"

