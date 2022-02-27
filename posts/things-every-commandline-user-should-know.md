# Things Every Command Line User Should Know

The command line is incredibly powerful. On the command line, you have full control over your computer. You can launch any program, move and copy any files, delete stuff, update, download, browse the web, poweroff or restart the system, etc. This is much more efficient than using the mouse and GUI programs to click through a bunch of menus and crap. If you're like me, and you use the command line on a daily basis, you'll want to read this! Some of these features are Bash only.


## set -o vi
One of the first things you should do when using the terminal on a Linux(or Unix) system is to decide whether you want to use emacs mode or vi mode. This decides how you move around on the command line, how you search in history and stuff like that. `set -o emacs` is the default, so if you want to stick to that, you can. I prefer `set -o vi`. I think it's super useful, especially since I'm a vim user and hence used to the keybindings.

Here's a quick little cheat sheet:

Emacs       Vi               Meaning
-----     ------            ---------
Ctrl+f      l                Move forward one character.
Ctrl+b      h                Move backwards one character.
CTRL+p      k                Move up (in history) once.
CTRL+n      j                Move down (in history) once.
Ctrl+a      0                Move to the beginning of the line.
Ctrl+e      $                Move to the end of the line.
Ctrl+k      d+$        Delete everything right of the cursor.
Ctrl+w      d+0        Delete everything left of the cursor.
Ctrl+r      /                Search in history(backwards in emacs).


Note: all of the Vi keys work in the *normal mode* not *insert mode*. You can read about the Vi modes if you want to understand that better. These are just some of the basic ones that's worth knowing. Remember that you can add `set -o vi` in your bashrc and have it load every time your load your bashrc. \


## Middle Mouse Button
What a lot of people don't know is that the mouse originally had three buttons. One left, one in the middle and one on the right. Technically, most mice still have three buttons, but the middle button just functions as a scroll wheel. It can still be mapped to stuff(even on Windows) in games and such. 

The middle mouse button was originally meant for pasting whatever you had selected. Microsoft Windows removed/never implemented this feature for whatever (dumb) reason. Linux(specifically the X11 display server) still has this feature. You can simply select something and then just middle click to paste the text you just selected. This is equivalent of doing Ctrl+C Ctrl+V except it's much quicker and easier. Linux does also support ctrl+C ctrl+V(or ctrl+Shift+C ctrl+Shift+V) for copying and pasting. This means that Linux has two clipboard buffers which is really awesome. 


## \\
This little backslash unaliases the command temporarily, allowing you to use the actual command.

For example, if I got top aliased to htop, and I do `\top` it will not execute htop, but top itself.

`alias htop="top"`

`top`

(I get htop)

`\top`

(I get top)


## >|
If you have noclobber enabled in your Bash shell, then you're unable to overwrite files. Well, with this little trick you can force it to overwrite existing files.

`echo "hi" > file`

bash: file: cannot overwrite existing file

`echo "hi" >| file`

`cat file`

hi


## $_
I use this *all* the time. It saves so much time. This is a special variable in Bash that expands to the last commands last argument.

`ls`

school-notes.md

`cat school-notes.md`

Some important school notes.

`rm $_`

The rm removes whatever argument you pass it. `$_` gets expanded to school-notes.md, so you removed school-notes.md without having retype it!


## !! and friends
The history commands that all start with an exclamation mark are quite nifty. Let's look at some of them:

### !!

`echo "hi"`

hi

`!!`

hi

`!!` expands to the last command executed in your bash history.


### !!:p

The :p prints out what *would* have been executed without actually executing it.

`echo "Hello 123"`

Hello 123

`!!:p`

echo Hello 123


### !-N


The N here can be replaced with any number you want. This will execute the command N commands ago.

`echo "Hey1"`

Hey1

`echo "Hey2"`

Hey2

`echo "Hey3"`

Hey3

`!-3`

Hey1

`!-3` here executes the command that got executed three commands ago.


You can even combine these like this:

`!-50:p`

This says "print(but do NOT execute) the command that ran 50 commands ago".


### !abc

`!echo` will run the last command that started with abc.

`echo "Hello World!"`

Hello World

`date`

Sat Jan 29 16:41:19 EET 2022

`!echo`

Hello World!


If you're eager to read more about history commands, check out [this](https://samrowe.com/wordpress/advancing-in-the-bash-shell/).


## \`\` or $()
\`\` and $() is known as command substitution in Bash. It runs the command you put inside it and returns the result, so you can do cool stuff like:

`vim $(mktemp)`

This will run the `mktemp` command -- which will output a temporary file -- and then open it in vim.

`ls -l $(which sh)`

lrwxrwxrwx 1 root root 4 Jan 16 10:45 /usr/bin/sh -> dash

This will run `which sh` -- which will output the path to sh -- and then do an `ls -l` on it.

Note: $() does the exact same thing as \`\`, but $() is preferred in shell scripts. \`\` is usually slightly faster to type on the command line depending on your keyboard.


## ${var## */}
This is called parameter expansion and is one of the most powerful things in Bash. There's too much to cover here, so if you want to read more about it, go and read the manual `man bash`

Let's say you have a variable that stores the path of a program and you want to just grab the programs name. Many people would use basename -- but that's not required. There's a more efficient way to do it:

`mypath="/usr/bin/grep"`

`program="${mypath##*/}"`

`echo $program`

grep


Again, go read about parameter expansion if you want to know more about it.


## shopt -s extglob
I have *no* idea why this isn't enabled by default. This is incredibly useful! This option enables extended globbing, which looks a bit like regex.

Let's say that you have three markdown files and two pictures in your directory:

`ls` 

file1.md file2.md file3.md photo1.jpg photo2.png

If you want to `ls` every file that does *not* end in .md, then you would do the following:

`ls !(*.md)`

photo1.jpg photo2.png


Let's look at another example:

`ls`

file1.md file2.md file3.md photo1.jpg photo2.jpg photo3.jpg photo4.jpg

`ls +(photo)+(2|3)+(.jpg)`

photo2.jpg photo3.jpg

This matches everything that starts with photo and is followed by either 2 or 3 and ends in .jpg. Isn't that awesome! It's like regex(almost). One big difference between regex and extended globbing is that the wildcard(+, ?, *, etc) comes BEFORE the pattern instead of AFTER(like in regex). Learn more about extended globbing [here](https://www.linuxjournal.com/content/bash-extended-globbing).




## shopt -s autocd
Do you ever feel like you keep typing cd a million times and you wish you didn't have to repeat it all the time? If this is the case, autocd is for you! `shopt -s autocd` allows you to just specify a directory without having to explicity type "cd" before the directory.

`cd Documents`

`shopt -s autocd` 

`Documents`

Same thing! It automatically cd's into Documents.


## CDPATH
You know when you have a PATH variable that Bash looks in when you try to run a program without specifying the full path? What if I told you that there's something similar but for the cd command? Let me introduce CDPATH. CDPATH is an environmental variable that checks for directories in the variable CDPATH when you cd into stuff that's not in your directory.

`CDPATH="$HOME/scripts"`

`cd Documents/whatever/work`

`pwd`

/home/bob/Documents/whatever/work

`cd scripts`

`pwd`

/home/bob/scripts


Wow! Would you look at that. It's like magic!



## Vi/Vim Magic
Speaking about magic, there's a way to send whatever you type in either the Vi or Vim text editor to any program that follows the Unix philosphy and then retrieve the output! That's the power of the Unix philosophy. This is why I **love** Unix. The Unix philosophy is about making many small programs that do one thing well and that sort of connect with each other(or communicate easily with each other) i.e they integrate well with other programs.

`vim file`

(inside vim now)

2 * 5 + 5

<pressing !! on the keyboard while on the same line as the equation>

(:.! appears in vim)

:.!bc

15

We just sent our current line to the bc program(bc is a cli calculator) and we received the output! Awesome! Try it out. It's truly incredible. You don't even have to exit Vim to communicate with other programs. Because Vi and Vim follow the Unix philosophy, they can easily send and receive data from here and there. This is similar to the concept of piping -- using a programs output as the input for another program -- in the sense that it has to do with the programs following the Unix philosophy and integrating well with other programs.



# Wrapping it all up

I only covered a fraction of the tricks and things every terminal user should know. There's many more in addition to these hiding in Bash. If you're interested in learning more, read the manual `man bash`.
