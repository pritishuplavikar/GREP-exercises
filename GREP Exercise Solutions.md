# GREP Exercise Solutions

## Multiple string match

1) Match lines containing either of these three strings
        String1: Not
        String2: he
        String3: sun
Solution: grep -e 'Not' -e 'he' -e 'sun' sample.txt

2) Match lines containing both these strings
        String1: He
        String2: or
Solution: grep 'He' sample.txt | grep 'or'

3) Match lines containing either of these two strings
        String1: a
        String2: i
   and contains this as well
        String3: do
Solution: grep -e 'a' -e 'i' sample.txt | grep 'do'

4) Match lines containing the string
        String1: it
   but not these strings
        String2: No
        String3: no
Solution: grep 'it' sample.txt | grep -vi 'no'

## Recursive search

Note: Every file in this directory and sub-directories is input for grep, unless otherwise specified

1) Match all lines containing the string: you
Solution: grep -r 'you'

2) Show only filenames matching the string: Hello
    filenames should only end with .txt 
Solution: grep -rl --include='*.txt' 'Hello'

3) Show only filenames matching the string: Hello
    filenames should NOT end with .txt 
Solution: grep -rl --exclude='*.txt' 'Hello'

4) Show only filenames matching the string: are
    should not include the directory: progs
Solution: grep -rl --exclude-dir='progs' 'are'

5) Show only filenames matching the string: are
    should NOT include these directories
            dir1: progs
            dir2: msg
Solution: grep -rl --exclude-dir='progs' --exclude-dir='msg' 'are'

6) Show only filenames matching the string: are
    should include files only from sub-directories
    hint: use shell glob pattern to specify directories to search
Solution: grep -rl 'are' */

## Search pattern from file

Note: words.txt has only whole words per line, use it as file input when task is to match whole words

1) Match all strings from file words.txt in file baz.txt
Solution: grep -f words.txt baz.txt 

2) Match all words from file words.txt in file foo.txt
    should only match whole words
    should print only matching words, not entire line
Solution: grep -owf words.txt foo.txt

3) Show common lines between foo.txt and baz.txt
Solution: grep -Fxf foo.txt baz.txt

4) Show lines present in baz.txt but not in foo.txt
Solution: grep -Fxvf foo.txt baz.txt

5) Show lines present in foo.txt but not in baz.txt
Solution: grep -Fxvf baz.txt foo.txt

6) Find all words common between all three files in the directory
    should only match whole words
    should print only matching words, not entire line
Solution: grep -owf words.txt foo.txt | grep -owf- baz.txt

## Regex

1) Match all lines containing any of these characters:
        character1: q
        character2: x
        character3: z
Solution: grep '[qzx]' sample_words.txt

2) Match all lines containing any of these characters:
        character1: c
        character2: f
    followed by any character
    followed by   : t
Solution: grep '[cf].t' sample_words.txt

3) Extract all words starting with character: s
    ignore case
    should contain only alphabets
    minimum two letters
    should be surrounded by word boundaries
Solution: grep -iowE 's[a-z]+' sample_words.txt

4) Extract all words made up of these characters:
        character1: a
        character2: c
        character3: e
        character4: r
        character5: s
    ignore case
    should contain only alphabets
    should be surrounded by word boundaries
Solution: grep -iowE '[acers]+' sample_words.txt

5) Extract all numbers surrounded by word boundaries
Solution: grep -ow '[0-9]*' sample_words.txt

6) Extract all numbers surrounded by word boundaries matching the condition
    30 <= number <= 70
Solution: grep -owE '[3-6][0-9]|70' sample_words.txt

7) Extract all words made up of non-vowel characters
    ignore case
    should contain only alphabets and at least two
    should be surrounded by word boundaries
Solution: grep -iowE '[b-df-hj-np-tv-z]{2,}' sample_words.txt

8) Extract all sequence of strings consisting of character: -
    surrounded on either side by zero or more case insensitive alphabets    
Solution: grep -io '[a-z]*-[a-z]*' sample_words.txt