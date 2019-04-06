# Forensics: Neo
## SwampCTF

This was a challenge in the forensics category from SwampCTF. This jpeg file is provided for the challenge:
<p align="center">
  <img src=red_pill.jpeg>
</p>

This steganography challenge is actually very simple. All that was needed was two commands:
<p align="center">
  <img src=commands.PNG>
</p>

Strings finds and prints any text strings embedded in files. I put that output into a text file to easily search for flags with grep.
And there we go, the flag is right there.
