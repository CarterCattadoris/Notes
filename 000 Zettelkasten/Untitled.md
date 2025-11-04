
Exercise 1:

#!/bin/bash

file=$1

cat "$file" > /dev/null
catStatus=$?

if [ $catStatus -eq 0 ]; then
        echo "cat: ok"
else
        echo "cat: ERROR"
fi

grep "TODO" "$file" > /dev/null
grepStatus=$?

if [ $grepStatus -eq 0 ]; then
        echo "grep: ok"
else
        echo "grep: ERROR"
fi


if [ $catStatus -eq 0 ] && [ $grepStatus -eq 0 ]; then
        exit 0
else
        exit 1
fi


Exercise 2:
ctrl+z puts it to the background, while ctrl+c terminates the process entirely

fg %2 brings back f2 since it was the second process we opened in the background