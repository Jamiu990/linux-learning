# Day 17 — Linux Filters and Text Processing Commands

Linux provides several commands for filtering, searching, extracting, sorting, and counting text. These commands are useful when working with files or processing the output of other commands.

## 1. `cut` — Extracting Parts of a Line

The `cut` command extracts specific characters or fields from each line of a file or input.

**Examples:**

```bash
cut -c1 filename
```
Displays the first character of every line.

```bash
cut -c1,3,5,7 filename
```
Displays characters at positions 1, 3, 5, and 7.

```bash
cut -c1-5 filename
```
Displays characters from position 1 to position 5.

```bash
cut -c1-3,6-8 filename
```
Displays characters from positions 1–3 and 6–8.

```bash
cut -b1-3 filename
```
Displays the first three bytes of every line.

**Note:** `-c` selects characters, while `-b` selects bytes. The `cut` command requires an option such as `-c`, `-b`, or `-f` to specify what to extract.

## 2. `awk` — Extracting and Processing Data

`awk` is a text-processing tool used to extract fields, filter lines, and perform simple operations on text.

By default, `awk` separates fields using spaces or tabs:
- `$1` — First field.
- `$2` — Second field.
- `$0` — The entire line.

**Examples:**

```bash
awk '{print $1}' filename
```
Displays the first field of every line.

```bash
ls -l | awk '{print $1, $3}'
```
Displays the file permissions and owner of each entry.

```bash
awk '!/Luffy/ {print}' filename
```
Displays lines that do not contain the word `Luffy`.

```bash
echo "Hello Tunde" | awk '{$2="Adam"; print $0}'
```
Replaces the second field (`Tunde`) with `Adam` and displays the result.

```bash
ls -l | awk '$9 == "reboot" {print $0}'
```
Displays the line where the ninth field (filename) is `reboot`.

## 3. `grep` and `egrep` — Searching Text

`grep` stands for **Global Regular Expression Print**. It searches through text and displays lines that match a specified pattern.

**Examples:**

```bash
grep "keyword" filename
```
Displays lines containing the specified keyword.

```bash
grep -c "keyword" filename
```
Counts the number of matching lines.

```bash
grep -i "keyword" filename
```
Searches without distinguishing between uppercase and lowercase letters.

```bash
grep -n "keyword" filename
```
Displays matching lines with their line numbers.

```bash
grep -v "keyword" filename
```
Displays lines that do not contain the keyword.

```bash
grep "keyword" filename | awk '{print $1}'
```
Finds matching lines and displays only their first field.

```bash
ls -l | grep "Desktop"
```
Displays directory entries whose output contains `Desktop`.

**Using `egrep`:**

`egrep` searches using extended regular expressions. It is useful when searching for multiple patterns.

```bash
egrep -i "keyword1|keyword2" filename
```
Searches for either keyword, ignoring uppercase and lowercase differences.

**Note:** `egrep` is an older form of `grep -E`. You can use the modern equivalent:

```bash
grep -Ei "keyword1|keyword2" filename
```

## 4. `sort` — Sorting Text

The `sort` command arranges lines in a file or input in a particular order. By default, it sorts alphabetically.

**Examples:**

```bash
sort filename
```
Sorts lines alphabetically.

```bash
sort -r filename
```
Sorts lines in reverse order.

```bash
sort -k2 filename
```
Sorts lines based on the second field.

## 5. `uniq` — Removing Duplicate Lines

The `uniq` command identifies repeated, adjacent lines. It is commonly used with `sort` to find or remove duplicates throughout a file.

**Examples:**

```bash
uniq filename
```
Removes consecutive repeated lines from the output.

```bash
sort filename | uniq
```
Sorts the lines and removes duplicates.

```bash
sort filename | uniq -c
```
Displays each unique line alongside the number of times it appears.

```bash
sort filename | uniq -d
```
Displays only lines that appear more than once.

**Note:** `uniq` only detects adjacent duplicate lines. Using `sort` first groups identical lines together.

## 6. `wc` — Counting Lines, Words, and Bytes

The `wc` command counts lines, words, and bytes in a file or input.

**Examples:**

```bash
wc filename
```
Displays the line count, word count, and byte count.

```bash
wc -l filename
```
Counts the number of lines.

```bash
wc -w filename
```
Counts the number of words.

```bash
wc -c filename
```
Counts the number of bytes.

**Using `wc` with pipes:**

```bash
ls -l | wc -l
```
Counts the lines in the output of `ls -l`. This normally includes the `total` line, so it may be one more than the number of listed entries.

```bash
ls -l | grep "drw"
```
Displays entries whose permission string contains `drw`.

```bash
ls -l | grep "drw" | wc -l
```
Counts the lines matching `drw`.

```bash
grep "keyword" filename | wc -l
```
Counts the number of lines containing the keyword.

**Important:** `wc` works with files and standard input, not directories directly. For example, `wc DIRECTORY` will normally return an error because a directory is not 
a regular text file.


## Summary

| Command | Purpose |
|---|---|
| `cut` | Extracts specific characters, bytes, or fields. |
| `awk` | Extracts and processes text fields. |
| `grep` | Searches for matching text patterns. |
| `egrep` / `grep -E` | Searches using extended regular expressions. |
| `sort` | Arranges lines in a specified order. |
| `uniq` | Identifies or removes adjacent duplicate lines. |
| `wc` | Counts lines, words, and bytes. |

## Key Takeaway

These commands become especially useful when combined with pipes (`|`). Instead of processing an entire file manually, you can pass the output of one command into another to search, filter, sort, and count information efficiently.