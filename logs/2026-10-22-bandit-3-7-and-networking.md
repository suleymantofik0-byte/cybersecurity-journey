# Bandit 3-7, Networking and TryHackMe (2026-10-22)

## Bandit
- Level 3: the password was in a hidden file inside the inhere folder. Plain ls
  showed nothing; ls -la showed ...Hiding-From-You. Read it with
  cat ./...Hiding-From-You. A dot at the start of a name only hides a file from
  the default view; it is not security.
- Level 4: ten files with names starting with a dash. file ./* shows the type
  of each by looking at its content, and only one was readable text. Using
  cat ./* would have dumped binary junk from the other nine.
- Level 5: 20 folders, and file ./* only said "directory". find searched all of
  them at once: find . -type f -size 1033c ! -executable.
- Level 6: the file could be anywhere on the server, so I searched from / with
  find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null.
  2>/dev/null throws away the "Permission denied" errors. Files have an owner
  (a user) and a group (a team of users); that pair identified my password file.
- Level 7: grep prints only the lines of a file that contain a word. find looks
  for files by properties like name and size; grep looks inside them.
- Connection dropped once and I lost my passwords. Now I save each one in a
  local file that never goes on GitHub.

## Mistakes I made (and what fixed them)
- Level 1: I typed .- and .bandit1/- before I understood ./- means "the file
  named - in this folder".
- Level 2: I typed "space" instead of "spaces" in the filename.
- Level 4: I tried find ./type text, but find does not read file contents; the
  file command does.

## Networking
- TTL is a number on each packet; every router subtracts 1 and the packet is
  dropped at 0. It stops loops. In DNS, TTL counts seconds instead.
- A VPN is an encrypted tunnel; a VPN concentrator is the device where all the
  tunnels end and get decrypted.
- ip route shows my default gateway, the first router my traffic goes to.
- ARP spoofing: an attacker makes my computer believe the gateway's IP belongs
  to the attacker's MAC address, so traffic passes through them.
- My Kali VM showed ttl=64 when I pinged, but Windows showed a different value.
  My hypothesis: a VM sits behind a virtual router, so VM results can differ.
  I have not confirmed this.

## TryHackMe
- Offensive Security Intro: used dirb on a practice bank site to find a hidden
  page nobody linked to.
- Defensive Security Intro: the SOC workflow is alert, triage, classify, contain,
  report. The alert was the same kind of scan I ran in the first room.



## Next
Bandit level 8, more Pre Security rooms, and my first Python tool.
