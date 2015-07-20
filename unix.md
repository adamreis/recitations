## Basic UNIX ##
 

### Paths ###
 
A good place to start with UNIX is the filesystem structure. Our macs run OSX, which is built upon a UNIX framework (just like Linux, ChromeOS and Android!). Unlike Windows machines, UNIX uses forward slashes to denote 
the break between directories and files. An example file path in UNIX might be 
`/usr/bin/dict`. The path `/` by itself denotes *the highest level directory*. 
If you start any path with a forward slash, it will assumed to be a path 
relative to the root directory `/`. Alternatively, your current directory is 
represented by the notation `./`. In most cases you can leave this off. You 
can find out your current directory using the command `pwd`. If you're current
directory is `/usr/bin` and you wish to reference the directory `/usr` in a
path, you can do so using *either* `/usr` (this is known as an absolute path),
or you can use `../` (this is a relative path. `../` denotes the directory above
the current directory. You could reference the root directory `/` from the
directory `/usr/bin` using the relative path `../../`.

### Basic Navigation ###

When you open Terminal, your current (working) directory will be
`/Users/<your username>`. Check this by **p**rinting the **w**orking **d**irectory:

    pwd

This is what's known as your home directory. You can do pretty
much whatever you want to the files in this directory. You own the place. Let's
**l**i**s**t all the files in the current directory:

    ls
    
See your `Desktop`? Let's move there! Use the **c**hange **d**irectory command. All three commands below will do the same thing (which ones are the
relative paths?)

	cd Desktop
	cd /Users/<your username>/Desktop
	cd ./Desktop

Let's make a new directory here. Use the `mkdir` 
command to **m**a**k**e a new **dir**ectory:

    mkdir makeschool 
    mkdir makeschool/learning

Now let's move into your working directory. 

    cd makeschool/learning

Let's create a new text file using the `touch` command. This will create
a new empty file if one does not exist, or update the last modified date if a
file exists.

    touch testing.txt
    touch .hidden.txt

Let's see if this worked. Try the `ls` command again. 
Some commands in UNIX take flags. These are special arguments
preceded by a dash. Usually it will make the most sense to attach the `-l` and
the `-a` flags to our ls calls. `-l` will include the permissions of each file
(more on this later) and `-a` will include files that are hidden (in UNIX, these
are files that start with a .)

    ls
    ls -l
    ls -l -a
    ls -la //we can combine flags for ls

Notice the differences in output each time the command is run. Now let's delete
our hidden file using the **r**e**m**ove command, `rm`.

    rm .hidden.txt
    ls -la

Now let's make a **c**o**p**y of `testing.txt`:

	cp testing.txt testing2.txt
	
`testing2.txt` is a boring name. Let's change it! There's no "rename" command in UNIX, but we can hack the **m**o**v**e command to do what we want:
	
	mv testing2.txt awesome.sauce

Alright, now lets get rid of the directory we created here. 

	cd ../
	rm learning

Uh oh! `rm` won't let you delete directories unless you specify to run it 
recursively (repeatedly go into each subdirectory and delete all files. It will
also ask for confirmation that you want to delete files unless you tell it to 
force the delete.  Luckily, rm accepts flags too. For force delete, use `-f` and for recursive use `-r`:

    rm -rf learning
    ls -la

One last thing as a side note: if you ever don't know how to use a command in
UNIX (or even a function in the standard C library) you can use the `man`
command. It will bring up the manual pages for the command you ask it for. Try
to learn more about the ls command:

    man ls

Use `q` to quit out of a man page.

### Useful Tricks ###
 
#### Tab Complete ####
 
When in bash, try to make use of *tab-complete* as often as possible. This just
means pressing tab after typing the first few letters of a command. For example
typing `tou` followed by the tab key will complete to `touch`. Tab complete also
works for directory and file names.

#### Previous command ####
 
You can go through your history by pressing the up and down arrows in terminal.
This will navigate between previously used commands so that you can easily use
the same commands over and over.

#### back i search ####
 
For long complicated commands that you only use every so often you can use the
reverse search to locate them in your history. Pressing `ctrl` `r` in terminal
will bring up a backward search through your history. Start typing until you
find the command you're looking for.


## Text Editors ##
 

There are two main text editors that you can use from inside terminal: emacs and
vim. Many programmers prefer these to traditional GUI-based text editors for several reasons. Primarily, they can get everything done in one window, they never have to take their hands off their keyboard, there are shortcuts for EVERYTHING, and they look way cooler. I, however, use Sublime Text (a GUI editor). It's also really popular -- it brings a lot of the great tools you'd expect with Vim and Emacs into a GUI that's much more similar to what you're used to with Microsoft Word. 

Which editor you use will ultimately be your decision (you could even write
everything in pico if you really wanted, but this would be difficult).

### Sublime Text###
http://www.sublimetext.com/
(I can give another talk on this if there's enough demand)

### Vim ###
 
Vim is a difficult to use text editor and very confusing at first. Its goal is
to be incredibly efficient by preventing unnecessary movement of your hands
around the keyboard. It operates in different modes, the most important of 
which will be *edit mode* and *insert mode*.

Open vim, editing a new file "vimtest".

    vim vimtest

When you open vim, it will be in Normal mode. Typing will cause a variety of
different operations to happen. For now switch to Insert Mode by pressing `i`.
You should see `-- INSERT --` appear at the bottom of the screen. At this point
anything you type will appear as text in the text file. This is fine for basic
editing. Now let's switch back to Normal mode. Press the `esc` key to switch
back.

Most vim commands execute as soon as you type them. Here are some basic commands
that will execute immediately:

  - `h` `j` `k` and `l` are how you move while in Normal mode. They are,
    respectively, left, down, up, right. Notice that this will save you time in
    moving to the arrows keys.
  - `dd` will delete the current line
  - `D` will delete from the current location to the end of the line
  - `yy` will copy the current line
  - `p` will paste whatever is the buffer (kind of like a clipboard)
  - `0` jumps to the beginning of the line
  - `$` jumps to the end of the current line
  - `w` jumps to the beginning of the next word (`W` uses a broader definition of word)
  - `b` jumps to the end of the previous word (likewise `B`)
  - `u` undoes the last change
  - `Ctl-r` redoes the last change

Some vim commands will not be executed until you press enter. These begin with a
colon.

  - `:w [optional filename]` This will save the current file if no file name is
    passed or write the current file to specified location.
  - `:x` This will save and quit
  - `:e filename` will open the filename specified
  - `:q` will quit vim and take you back to terminal
  - `:[line numer]` will jump to that line

That should be enough for basic vim navigation. If you want to learn to be a
real vim ninja, get used to switching between modes first. Then try to expand
your Normal mode vocabulary one command at a time.

In vim, most commands work with some sort of combination between prepositions
and actions. For example, `gg=G` would indent the entire file, as `gg` takes you
to the beginning of the file, `=` auto-indents a line, and `G` jumps to the end
of the file. 

You can also use *vimtutor* to really learn the ins and outs. In terminal, just
type

    vimtutor

Alternatively, check out [Open Vim's Tutorial](http://www.openvim.com/tutorial.html)
for another interactive vim lesson. Or play a little NES Zelda type game while
learning vim, with [Vim Adventures](http://vim-adventures.com/).

After learning vim, you might want to configure it. This is done by editing the
.vimrc file in your home directory. Let's check out our current settings.

    vim ~/.vimrc

There should be default settings there already, but you can look to make changes
here in the future. Jae and the TAs will send out their configurations later,
but a good starting point is to enable line numbers by adding this line to your
vimrc:

    set number


### Emacs ###
*May be skipped for time*
 
Emacs is an easier to pick up text editor but has less efficient keyboard
shortcuts compared to vim.

Let's start by editing a new file in emacs

    emacs emacstest

As soon as emacs starts running, you will be able to type into it. There is no
special insert mode like in vim. You can backspace at any time without having to
switch between modes.

Emacs has much of the functionality that vim has and we present the basics below:
  
  - 'Ctrl-f' will move your cursor forward, 'Ctrl-b' will move it back, 'Ctrl-p'
    will move it up, 'Ctrl-n' will move it down
  - 'Ctrl-k' will delete the current line
  - 'Ctrl-s' will search for a word forward, 'Ctrl-r' will search for a word backward
  - 'Ctrl-a' goes to beginning of line, 'Ctrl-e' goes to end
  - 'Ctrl-spacebar' to select text to manipulate
  - 'Esc-w' to copy text, 'Ctrl-w' to cut text, Ctrl-y' will paste your most
    recently copied/deleted text
  - 'Esc-g g' then enter a line number to jump to a particular line in the buffer

To exit and save we will use Ctrl-X + Ctrl-C. If you just want to save then use
Ctrl-X + Ctrl-S.

Just like vim, emacs also has a configuration file that you can edit. This is
.emacs file within your home directory. Let's check out our emacs settings.

    emacs ~/.emacs

There should be default settings there already, but feel free to add more for
shortcuts.

*Note that backspaces can be a little funky when ssh-ing into CLIC and your
*backspace button might actually be sending "Ctrl + H" instead! To fix this you
*will have to add the following lines to your .emacs file.

    ;; make sure backspace deletes backwards
    (normal-erase-is-backspace-mode 1)
    ;; make sure your backspace is mapped correctly
    (global-set-key "\C-h" 'backward-delete-char)
