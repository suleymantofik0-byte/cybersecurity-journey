# Bandit 9-11 and TryHackMe Networking (2026-10-27)

## Bandit
- Level 9: the password was mixed into mostly binary junk. The strings command pulled out only the human-readable text, and grep then filtered those lines down to the ones containing the = characters the goal mentioned.
- Level 10: the file was base64-encoded, not encrypted. base64 -d decoded it.
  Base64 isn't a secret, it's a public way to write binary data as text so it
  can travel through systems built for plain text (like email).
- Level 11: the file was encrypted with ROT13, a cipher that shifts each letter
  13 places through the alphabet. I built tr 'A-Za-z' 'N-ZA-Mn-za-m' by writing
  out both alphabets on paper first: normal A-Z on one line, then the same
  alphabet starting at N underneath, wrapping around after Z. Running it twice
  returns the original text, since 13 + 13 = 26.

## TryHackMe: What is Networking?
- MAC address spoofing: a router in the lab only let in a specific allowed MAC
  address. I changed my simulated device's MAC to the allowed one and got
  through. This works because a MAC address is just a value reported by
  software, not something physically locked.
- Explored a live Wireshark capture: saw MDNS/SSDP broadcast traffic where
  devices on a shared network constantly announce themselves, and found MAC
  addresses inside the Ethernet II layer of a packet.
- Learned the word "syntax": the required order and structure of a command,
  separate from what the words mean. Example: ping -c 4 10.10.10.10 has a
  fixed shape (command, option, value, target) and typing it out of order or
  with wrong spacing breaks it, even if every piece is individually correct.

## What confused me
I understood ROT13 as an idea quickly, but building the actual tr command confused me because I didn’t see how the two character sets line up position-by-position. I had to write both alphabets out on paper before it clicked

## Next
Finish What is Networking?, then Bandit level 12, then start Python.
