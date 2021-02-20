# Linux Stream-EDitor (SED) + PERL + AWK

In this document we're going to go through some of the mostly used methods of text manipulation in Linux operating systems. These methods do not just apply to Linux but they originate form there. 

## SED

The first thing we're going to explore is the popular `sed` command.

```bash
sed 's|FIND_TXT|REPL_TXT|'    # FIND_TXT --> REPL_TXT
sed 's/FIND_TXT/REPL_TXT/3'    # FIND_TXT --> REPL_TXT    
sed 's|FIND_TXT|REPL_TXT|g'    # FIND_TXT --> REPL_TXT
sed -i 's|FIND_TXT|REPL_TXT|g' file.txt # Applies changes directly to the file
```

By ``sed -E`` we can use extended regular expressions : (matching-groups, all operators)

```bash
echo 'Hello   World.' | sed -E 's|Hello +(.*).|\1|g'
>> World
```

## SED + Multiline !

We have a text like this: 

```
FirstLine
SecondLine
ThirdLine
FourthLine
```

#### Method-1

We can apply the following `sed` operation to change the `SecondLine` and the `ThirdLine` all together.

```bash
sed -e '1h;2,$H;$!d;g' -e 's|SecondLine\nThirdLine|2and3Repl|g' 
```

#### Method-2

By default `sed` ends its search when it reaches the newline `\n` character. We can temporarily replace that character and treat the text as a single-line string and the revert changes to the `\n`:

```bash
tr '\n' '\0' | sed 's|SecondLine.*ThirdLine|REPL|g' | tr '\0' '\n'
```

#### Method-3

Use **PERL**! Perl makes it simple to do multiline text manipulation, why?? Well Perl is a programming language same as Python but it's already installed on most Linux distros and it has internal support for regex. Regular expressions are a fundamental base of the Perl programming language.

```bash
perl -0777 -pe 's|Second.*rdLine|REPL|igs'
```

Output:

```
FirstLine
REPL
FourthLine
```

## AWK

`awk` is a scripting language which is the standard tool supported by Linux for text manipulation. It is very powerful in terms of dealing with text with different criteria's. Here we'll explore some of the main features and commands available in `awk`:  
[How to use regular expressions in awk | Opensource.com](https://opensource.com/article/19/11/how-regular-expressions-awk)

General format of `awk` command : `` awk [options] '_CONDITIONS_ {_ACTIONS_}' ``

```bash
awk '/^st/' # Show lines that start with 'st' # Regular Expressions go inside slashes '/regex/'
awk '$3 ~/^st/' #Regex is applied to the third column 
awk '! /:$/' # Show only lines that do not end with ':'
awk -F: '{print $1}' # Print only the first col. Actions go inside curly-braces. Default seperator is ' ' but it can be changed using -F which here is change to colon ':'.
awk -F: '$3 > 1000' # Third col. value bigger than 1000. This is of type Condition.
awk -F: '/^s/ {print $1,$3*100"M"}' #Conditions and Actions can be combined this way. Here third col value is multiplied by 100 and then, character "M" is added to the end of it.
awk '/.png/ && $5/1024 > 10 {print $9,int($5/1024)" KB"}' #Conditions are combined with && and int() function rounds up the number.
awk '$1/1024>10 && $2 !~ /keepit/ {print $1/1024"M",$2}' #Combination of a condition for first col and (not)regex on the second col and an action to print the results
```

* awk scripts could be written and executed from a file.
* It is possible to define functions in awk using the `function x()` keyword.

## REGEX

`^Action.*?Stop.*?$` -> here `.*?` looks for the smallest possible match (non-greedy)

`/.+?(?=world)/` -> matches every that come before the word `world`

## RESOURCES

Regex Online Tool : [regex101: build, debug and test regex](https://regex101.com/)

SED Commands :

```
:  # label
=  # line_number
a  # append_text_to_stdout_after_flush
b  # branch_unconditional             
c  # range_change                     
d  # pattern_delete_top/cycle          
D  # pattern_ltrunc(line+nl)_top/cycle 
g  # pattern=hold                      
G  # pattern+=nl+hold                  
h  # hold=pattern                      
H  # hold+=nl+pattern                  
i  # insert_text_to_stdout_now         
l  # pattern_list                       
n  # pattern_flush=nextline_continue   
N  # pattern+=nl+nextline              
p  # pattern_print                     
P  # pattern_first_line_print          
q  # flush_quit                        
r  # append_file_to_stdout_after_flush 
s  # substitute                                          
t  # branch_on_substitute              
w  # append_pattern_to_file_now         
x  # swap_pattern_and_hold             
y  # transform_chars
```

[[Appendix A\] A.3 Command Summary for sed (mik.ua)](https://docstore.mik.ua/orelly/unix/sedawk/appa_03.htm)

