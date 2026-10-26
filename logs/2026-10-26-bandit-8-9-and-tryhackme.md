# Bandit 8-9 and TryHackMe (2026-10-26)

## Bandit
- Level 8: the password was the one line that appears only once in a big file.
  sort data.txt | uniq -u worked. uniq only notices repeats on neighbouring
  lines, so sort has to come first. Plain uniq removes repeats but keeps one
  copy of every line; the -u option shows only lines that were never repeated.
- Level 9: [only if finished: strings pulls readable text out of a binary file,
  and grep filtered the lines I needed. cat would have dumped junk.]
- Mistake: I ran uniq --help data.txt, but --help always wins and just prints the
  help again. The option has to go where --help was.
- Learned to read a help screen: each option has a short form (-u) and a long
  form (--unique), and the right column says what it does.

## TryHackMe
- Careers in Cyber: the quiz suggested Incident Responder. I also read the
  Penetration Tester page: [one sentence in my own words about what a pentester does].
- Inside a Computer: [one or two sentences in my own words about what the CPU,
  RAM and storage do, and why this matters when investigating a seized computer].

## Other
- I registered for a local cybersecurity discussion event but had a class at that
  time. Lesson: check my timetable before registering.

## Next
Bandit level 10, TryHackMe "What is Networking?", and my first Python tool.
