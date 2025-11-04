
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
