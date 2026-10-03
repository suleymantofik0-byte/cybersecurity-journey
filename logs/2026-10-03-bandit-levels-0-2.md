# Bandit Levels 0-2 (2026-10-03)

## What I learned
- OverTheWire Bandit is a practice game: a real Linux server with a password 
  hidden at each level, built for legal practice.
- SSH lets me control another computer's terminal securely over the network.
  Command: ssh bandit0@bandit.labs.overthewire.org -p 2220
  (ssh = program, bandit0 = username, the address = the server, -p 2220 = port)
- ls lists names inside a folder. cat shows the text inside a file.
- ls -l shows the type in the first character: "-" means file, "d" means folder.

## Level 1: file named "-"
- The password file was literally named "-".
- cat - waits for keyboard input, because a lone "-" means "read from keyboard".
- Fix: cat ./-  (the ./ makes it a path, so cat treats it as a file)

## Level 2: spaces in the filename
- The file was named "--spaces in this filename--".
- Spaces split a name into separate arguments, so cat saw four different files.
- Fix: cat ./--spaces\ in\ this\ filename--
  (backslash before each space, plus ./ because the name starts with --)
- Quotes around the whole name also work.
- Tab completion types the backslashes for me.

## What confused me
[i am getting connfused with linux but i am getting throught it]

## Next
Bandit level 3, then keep going toward level 15.
