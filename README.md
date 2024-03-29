# AutoCompete
This repo has moved to: <https://github.com/geluso/autocompete-programming-contest>

## Rules
* Up to three people per team
* Only one computer per team
* Pen and paper will be provided
* Internet access is allowed (though probably mostly unuseful)
* No third party libraries (no gems, no pip, no npm, etc)
* You may solve problems in any order
* Rankings are ordered by the number of problems solved and time taken

## Sample Boiler Plate
All of the programs are required to read input from STDIN (standard input).
Each language has it's own way of accessing this input. Here are samples to
get you started. You can use this boilerplate to build the rest of your
programs around, or read from STDIN any other way you wish.

If you have a text file called `input` and a program called `foo` (in whatever
language) you can have the program read the file input by executing the
following in your bash terminal. The `cat` command prints the contents of
the `input` file and "pipes" the output as input for your program. Your program 
reads from STDIN and reacts to the input.

```
cat input | python foo.js
cat input | ruby foo.rb
cat input | node foo.js
```

Try this out to make sure your programs execute correctly!

**Python 3**
```py
import fileinput
for line in fileinput.input():
  print(line)
```

**Ruby**
```ruby
lines = ARGF.read.split("\n")
lines.each do |line|
  puts line
end
```

**JavaScript**
```js
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
  terminal: false
});

const lines = []
rl.on('line', (line) => lines.push(line));
rl.on('close', (line) => process(lines));

function process(lines) {
  console.log(lines)
}
```

<div style="page-break-after: always;"></div>

## Problems

### dlroW olleH
Write a program in a file called `hello` that reads from standard input. Your
program should reverse each line and print it back out.

Sample Input

```
hello
world
```

Sample Output

```
olleh
dlrow
```

### N-ibonacci
Write a program in a file called `nib`.

The program should compute fibonacci-like sequences. Fibonacci is defined as a sequence
of numbers where each number is the sum of the last two previous numbers. The
very first two numbers in the sequence are `1` and `1`.

```
fib(1) = 1
fib(2) = 1
fib(3) = 1 + 1 = 2
...
fib(n) = fib(n - 1) + fib(n - 2)
```

Write a program that builds on the idea of the fibonacci sequence. Instead of the
sequence adding up just the last `2` numbers modify it so it adds up the last `L`
numbers. "N-ibonacci."

`nib(L, n)` means return the `nth` number in the sequence, where you add up the last
`L` numbers. The first `L` numbers in the sequence are always `1`.

The original fibonacci sequence would look like this, with `L=2` because it adds the
last two numbers:

```
nib(L=2, 1) = 1
nib(L=2, 2) = 1
nib(L=2, 3) = 1 + 1 = 2
...
nib(L=2, n) = nib(L=2, n - 1) + nib(L=2, n - 2)
```

N-ibonacci with `L=3` would look like this. It starts with three `1` ones and
the next number is always computed by adding up the last three numbers.

```
nib(L=3, 1) = 1
nib(L=3, 2) = 1
nib(L=3, 3) = 1
nib(L=3, 4) = 1 + 1 + 1 = 3
nib(L=3, 5) = 1 + 1 + 3 = 5
...
nib(L=3, n) = nib(L=3, n - 1) + nib(L=3, n - 2) + nib(L=3, n - 3)
```

N-ibonacci defines all numbers with `L=1` as `1` because the first number in the
sequence is `1` and all next numbers are equal to just the last number.

```
nib(L=1, 1) = 1
nib(L=1, 2) = 1 = 1
...
nib(L=1, n) = nib(L=1, n - 1)
```

N-ibonacci defines all numbers in the sequence for `L < 1` as simply `0`.

The program input consists of lines containing two numbers separated by a
space. The first number represents the value of `L`. The second number
represents the value of the `nth` number to return in that sequence. Your
program should compute `nib(L,n)` for each line and print the result.

`n` is always guaranteed to be `n >= 1`.

Sample Input
```
2 1
2 2
2 3
2 4
2 5
2 6
3 1
3 2
3 3
3 4
3 5
```

Sample Output
```
1
1
2
3
5
8
5
1
1
1
3
5
```

<div style="page-break-after: always;"></div>

### Cipher
Write a program in a file called `cipher` that accepts a cipher mapping
relating each letter of the alphabet to another letter. Use the cipher mapping
to decode and print a provided message.

The first two lines of the file are the cipher mapping. The remaining file
contents are the encoded message.

Sample Input

```
qwertyuiopasdfghjklzxcvbnm
zxcvbnmqwertyuiopasdfghjkl
owsn gwx
r lrk r esrk r grkrs erkrlr
```

Sample Output
```
holy cow
a man a plan a canal panama
```

### Tag
Write a program in a file called `tag` that simulates people playing tag. The
first line contains an integer `N` describing how many people are playing the
game. The next `N` lines describe each of the `N` players. Each line consists
of a letter and two integer coordinates describing the players' `row col`
position. The first player listed is "it." They're trying to tag other players
by moving in to their square.

The remaining lines describe player movement. Each line describing movements
starts with a player's symbol, then their direction of movement. If the "it"
player attempts to move on to the position of another player it counts as a
tag. The tagged player becomes "it" and all players keep their positions.

You may assume (besides tagging) players never attempt to move on to each other's
cells.

The grid is defined by rows and columns. All row and column indexes are integers.
There is not limit to the range of the size of the grid.

You can think of (0,0) as (row, col) and the following transformations:

* (0,0) after "up" is (-1,0)
* (0,0) after "down" is (1,0)
* (0,0) after "left" is (0,-1)
* (0,0) after "right" is (0,1)

Your program should print out the series of tags that happen in the game like
`A tags B` then `B tags C` and so forth.

Sample Input

```
4
A 0 0
B 1 0
C 0 3
D 2 1
A down
B right
B right
C up
B right
B up
```

Sample Output

```
A tags B
B tags C
```

### Minesweeper
Write your program in a file called `sweep`.  Given a 2D grid filled with
either periods `.` or asterisks `*` print out Minesweeper markings for the
board. Each space containing an asterisk should remain an asterisk. Every other
space should contain a digit representing how many asterisks that space is
touching.

Sample Input

```
........
.*......
........
........
***...*.
*.*..*..
***.....
........
```

Sample Output

```
11100000
1*100000
11100000
23210111
***212*1
*8*31*21
***21110
23210000
```

<div style="page-break-after: always;"></div>

### Cave
Write your program in a file called `cave`.  Given a block of 2d text determine
how many different "caves" their are.  You are guaranteed that the map of caves
has a complete border of `#` pound signs.  There are never cave edge ` ` empty
spaces that touch the edge.

Sample Input
```
################################################################
##########################################  ####################
##########  #############################    ###################
#########    ############################    ###################
#########    ############################   ####################
##########    ###########################   ####################
##########    ###########################    ###################
#########    ############################     ###  #############
#######      ############################           ############
#####         ########   ################           ############
####          #######     ###############       ##   ###########
####          ######       #############       ####    #########
#####        #######       #############      #####     ########
######    ###########      ############      #####       #######
#######  #############     ############      ####         ######
#######################    ####   #####      ####         ######
#######################     ##     ####      #####        ######
#######################            #####    ########      ######
########################          #######   #########     ######
########################          ########  #########     ######
########################         #########  ##########   #######
########################         #########   ###################
##############  ########         #########    ##################
#############    ######          #########     #################
###########              ##     #########      #################
##########              ####  ###########      #################
##########              #################     ##################
##########               ########   ####      ##################
###########              #######              ##################
############             #######             ###################
#################       #########         ######################
################################################################
```

Sample Output
```
3
```

<div style="page-break-after: always;"></div>

### Fuzz Bizz
Write your program in a file called `buzz`.

The first line contains two integers. The second line contains two words. The
rest of the lines contain integers.

If any of the lines (beside the first two) is evenly divisible by the first number
print just the first word. If a number is evenly divisible by the second number print
just the second word. If a number is evenly divisible by both numbers print out the
first word then the second word. If the number is not evenly divisible by either
of the first two numbers simply print the number.

You may assume all numbers are greater than zero.

Sample Input

```
3 5
Fuzz Bizz
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
```

Sample Output

```
1
2
Fuzz
4
Bizz
Fuzz
7
8
Fuzz
Bizz
11
Fuzz
13
14
Fuzz Bizz
16
17
```

