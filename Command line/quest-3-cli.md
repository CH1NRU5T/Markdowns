# Quest - 3

## Part 1 - Using Wildcards to Search for Files

## An introduction to using wildcards

- When searching for files on your computer, you can use **wildcards** to represent unknown characters or match particular character sets.
- wildcard takes place of an unknown or a set of unknown characters (like regex).
- can be used with `ls` or `rm` to list or remove files matching a given criteria.
- Commonly used wildcards:
  - `?`
  - `*`
- `*`

  - represents any number of unknown characters
  - used when we have partial names for docs or files
  - for example:
    - `cheese*` might return:
    - cheese
    - cheesecake
    - cheesedip.txt
      <br>
    - `*cheese` might return:
    - stringcheese
    - swisscheese
    - sliced.cheese
      <br>
    - `*.extension` to search for files with specific extension \
    - `*.txt`

- `?`

  - represents only **1** unknown character
  - for example:
    - `take?.txt`:
      - take1.txt
      - taken.txt
      - take2.txt
      - it will not find take12.txt coz `?` searches only for 1 element (`take??.txt` can be used to find it)

- Combining `*` and `?` - for example: - `home??.*`: - home45.bak - homer4.txt - not found -> homeloan.doc
  <br>

## 10 practical uses of wildcards

- `$ ls l[abdcio]st.sh`
  - matches all files with names starting with l followed by any of the characters in the square bracket but ending with st.sh
- `$ ls users-[0-9][a-z0-9][0-9]*`
  - match starting with users-i, followed by a number, a lower case letter or number, then a number and ends with one or more occurences of any characters
- `$ ls users-[0-9][a-zA-Z0-9][0-9]*`
  - match begin with users-i followed by a number, a lower case or upper case character or number, then a number and then ends with one or more occurences of any character.
- `$ ls users-[0-9][!0-9][a-zA-Z]*`
  - starting with users-i, followed by a number, any valid file naming character from number, a lower case or uppercase character and then ends with one or more occurences of any character.

<br>
<br>

## Part 2 - Combining Commands with Pipes

- Piper allow you to combine two or more commands in the same line.
- output of first command is used as input for second command and so on.
- syntax: `command1|command2`
- example:
  - `ls|more`
    - more command takes input from ls command and appends it to the standard output.

#### Common filters

- `grep`, `more`, `sort`
- `grep`:
  - pattern or expression matching command
  - searches for a pattern or regex that matches files or directoriesand then prints out found matches.
  - syntax: `$grep[options] "**pattern to be matched**" filename`
  - `$grep 'hello' ist_file.txt`: searches hello in ist_file.txt and returns the lines containing 'hello'.
  - `$grep 'hello' *`: searches for hello in all files and directories
  - Options in `grep` command:
    - `-v`: returns all lines that do not match specified regex
    - `-n`: returns all lines that match specified regex along with line number.
    - `-l`: returns only the names of files matching the specified regex
    - `-c`: returns count of lines that match specified regex
    - `-i`: case sensitive option and matches either lowercase or uppercase.
- `sort`:
  - data manipulation command
  - sorts or merges lines in a file by specific fields.
  - sorts the lines of text alphabetically or numerically
  - default alphabetical
  - syntax: `$ sort[options] filename`
  - `sort` options:
    - `-n`: sorts lines in numerical order
    - `-r`: reverses the order of sorting
    - `-f`: sorts uppercase and lowercase together
    - `+x`: dosent consider ist x fields while sorting.
  - example:
    - `$ sort fruits.txt`
    - `$ sort -n grades.txt`
- `more`: - customize the displaying contents of file - displays text file contents on terminal with paging controls - to display next line - `enter` - bring up next screen - `spacebar` - move to next file - `n` - quit - `q` - syntax: `$ more[options] filename` - example: - `cat fruits.txt | more` - While using more command, the bottom of the screen contains more prompt where commands are entered to move through the text.
  <br>

## Part 2 - Combining Commands with Pipes

- `grep`: **global search for regular expression and print out**
  - the grep filter searches a file for a particular pattern of characters, and displays all lines that contain that pattern.
  - The pattern that is searched in the file is referred to as the regular expression
  - `$ grep [options] pattern [files]`
  - Options:
  - `-c`: this prints only a count of the lines that match a pattern
  - `-h`: display the matched lines, but do not display the filenames.
  - `-i`: ignores, case for matching
  - `-l`: displays list opf filenames only
  - `-n`: display the matched lines and their line numbers
  - `-v`: prints out all lines that do not match the pattern
  - `-e <exp>`: specifies expression with this option, can use multiple times.
  - `-f <file>`: takes patterns from files, one per line.
  - `-E`: treats patern as extended regular expression **(ERE)**
  - `-w`: Match whole word.
  - `-o`: prints only the matched parts of a matching line, with each such part on a separate output line.
  - `-A n`: prints searched line and n lines after the result
  - `-B n`: prints searched line and n line before the result
  - `-C n`: prints searched line and n lines after before the result

#### Some searches

- **Case insensitive search**:
  - `$ grep -i "UNix" geekfile.txt`
- **Displaying the count of number of matches**:
  - `$ grep -c "unix" geekfile.txt`
- **Display the file names that matches the pattern**:
  - `$ grep -l "unix" *`
- **Checking for the whole words in a file**:
  - `$ grep -w "unix" geekfile.txt`
- **Displaying only the matched pattern**:
  - `$ grep -o "unix" geekfile.txt`
- **Show line number while displaying the output using grep -n**:
  - `$ grep -n "unix" geekfile.txt`
- **Inverting the pattern match**:
  - `$ grep -v "unix" geekfile.txt`
- **Matching the lines that start with a string**:
  - `$ grep "^unix" geekfile.txt`
  - The ^ regular expression pattern specifies the start of a line.
- **Matching the lines that end with a string**:
  - `$ grep "os$" geekfile.txt`
  - The $ regular expression pattern specifies the end of a line.
- **Specifies expression with -e option. Can use multiple times**:

  - `$ grep –e "Agarwal" –e "Aggarwal" –e "Agrawal" geekfile.txt`

  - output:
    ```
    Agarwal
    Aggarwal
    Agrawal
    ```

- **Print n specific lines from a file**:
  - output:
    ```
    $grep -A[NumberOfLines(n)] [search] [file]
    $grep -B[NumberOfLines(n)] [search] [file]
    $grep -C[NumberOfLines(n)] [search] [file]
    ```
  - example:
    - `$ grep -A1 learn geekfile.txt`
- **Search recursively for a pattern in the directory**: - `$ grep -iR geeks /home/geeks` - output:
  ` ./geeks2.txt:Well Hello Geeks ./geeks1.txt:I am a big time geek ---------------------------------- -i to search for a string case insensitively -R to recusrively check all the files in the directory. `
  <br>

## Part 4 - Transferring Data to or from a Server

- `curl` - **client URL**
- _curl_ is a command-line tool to transfer data to or from a server, using any of the supported protocols (HTTP, FTP, IMAP, POP3, SCP, SFTP, SMTP, TFTP, TELNET, LDAP, or FILE).
- syntax: `curl [options] [URL...]`
- `curl https://www.geeksforgeeks.org`
- Options:
  - `-o`:
    - saves the downloaded file on the local machine with the name provided in the parameters.
    - `curl -o [file_name] [URL...]`
    - `curl -o hello.zip ftp://speedtest.tele2.net/1MB.zip`
  - `-O`:
    - This option downloads the file and saves it with the same name as in the URL.
    - `curl -O [URL...]`
    - `curl -O ftp://speedtest.tele2.net/1MB.zip`
  - `-C`
    - This option resumes download which has been stopped due to some reason. This is useful when downloading large files and was interrupted.
    - `curl -C - [URL...]`
    - `curl -C - -O ftp://speedtest.tele2.net/1MB.zip`
  - `-limit-rate`:
    - This option limits the upper bound of the rate of data transfer and keeps it around the given value in bytes.
    - `curl --limit-rate [value] [URL]`
    - `curl --limit-rate 1000K -O ftp://speedtest.tele2.net/1MB.zip`
  - `-u`:
    - curl also provides options to download files from user authenticated FTP servers.
    - `curl -u {username}:{password} [FTP_URL]`
    - `curl -u demo:password -O ftp://test.rebex.net/readme.txt`
  - `-T`
    - This option helps to upload a file to the FTP server.
    - `curl -u {username}:{password} -T {filename} {FTP_Location}`
    - If you want to append an already existing FTP file you can use the `-a` or `–append` option.
  - `-libcurl`:
    - This option is very useful from a developer’s perspective. If this option is appended to any cURL command, it outputs the C source code that uses libcurl for the specified option. It is a code similar to the command line implementation.
    - `curl [URL...] --libcurl [filename]`
  - `-x`, `-proxy`:
    - curl also lets us use a proxy to access the URL.
    - `curl -x [proxy_name]:[port] [URL...]`
    - `curl -u [user]:[password] -x [proxy_name]:[port] [URL...]`
  - **Sending mail** - As curl can transfer data over different protocols, including SMTP, we can use curl to send mails.
    `curl –url [SMTP URL] –mail-from [sender_mail] –mail-rcpt [receiver_mail] -n –ssl-reqd -u {email}:{password} -T [Mail text file]`
  - **DICT protocol:**
    - The Libcurl defines the DICT protocol which can be used to easily get the definition or meaning of any word directly from the command line.
    - `curl [protocol:[dictionary_URL]:[word]`
    - `curl dict://dict.org/d:overclock`
