# PHP strpos() False Positive Bug

This repository demonstrates a common, yet subtle, bug in PHP code related to the `strpos()` function and loose comparison. The `strpos()` function returns `false` if the needle is not found, however this is also loosely equal to 0 which is a valid position.

The bug arises when checking the return value of `strpos()` for the presence of a substring using loose comparison (`==`). This can lead to false positives if the substring is located at the beginning of the string, as `strpos()` will return 0, which is evaluated as true in the condition `strpos(...) == 0`.

## Bug

The `bug.php` file demonstrates this bug. It attempts to check if a needle is present at the beginning of a haystack but can lead to false positives. 

## Solution

The `bugSolution.php` file shows the correct way to handle this case by using strict comparison (`===`) to avoid the loose comparison issue.  This ensures that only the exact value `false` will cause the `else` block to execute. 

## How to reproduce

Clone this repository and run the `bug.php` file using a PHP interpreter. It will print 'Needle found at the beginning!' even when the needle is not present, only at the start of the string. Then run the `bugSolution.php` file to see the correct output.