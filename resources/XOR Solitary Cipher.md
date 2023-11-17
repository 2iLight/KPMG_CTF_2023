# XOR Solitary Cipher

In the distant future, on the mysterious planet of Zenthia, a lone adventurer named Maya discovered an ancient artifact known as the XORbit. This enigmatic device held immense power and could only be activated with a single character key. As she embarked on a perilous quest to decipher the code, dark forces from across the galaxy pursued her, eager to harness the XOR bit's abilities for their malevolent intentions. Help her decrypt the message.

**Points - 150**

Cipher text:

```plaintext
06216f3b272a6f3d2a2e23226f20296f2c202b2a3c6f2e212b6f2c3d363f3b262c6f2e3d3b634518272a3d2a6f2226212b3c6f3a21263b2a636f2e6f2c272e23232a21282a6f3b206f26223f2e3d3b61450c1b09636f2e6f3e3a2a3c3b6f29203d6f3b272a6f2c3a3d26203a3c6f3c203a2363451f3a3535232a3c6f3b206f3c2023392a636f3b272a6f22363c3b2a3d262a3c6f3a212920232b6145450d363b2a3c6f2b2e212c2a6f2e212b6f242a363c6f3827263c3f2a3d6f3c2a2c3d2a3b3c6f3a213b20232b634506216f3b27263c6f2b2628263b2e236f2e3d2a212e636f272a2e3d3b3c6f2e3d2a6f2d20232b6145072e2c242a3d3c6f2e212b6f3b272621242a3d3c636f3b20282a3b272a3d6f3b272a366f3c3b3d26392a63451b206f2c20213e3a2a3d6f3b272a6f29232e283c636f2e212b6f3b272a6f2823203d366f2b2a3d26392a61454506216f2a392a3d366f2c272e23232a21282a636f24212038232a2b282a6f263c6f282e26212a2b634506216f0c1b09683c6f2b20222e2621636f3f2e3c3c2620213c6f3a212c272e26212a2b6145042a366f263c6f041f0208340c3d363f3b262c102e3d3b103a212920232b2a2b32
```

Given that the given cipher is an XOR cipher, lets code a program to decipher it.

Python script : [XOR_decode.py](/resources/XOR_decode.py)

The script defines a function `xor_decode` that takes an encoded hex string as input and returns a list of tuples containing the key used for decoding and the decoded message. The function works by performing a brute-force XOR decryption with all possible keys (0-255) and then trying to decode the resulting bytes using UTF-8.

For key _0x4F_ the output is:

```plaintext
Key: 0x4f, Decoded Message: In the realm of codes and cryptic art,
Where minds unite, a challenge to impart.
CTF, a quest for the curious soul,
Puzzles to solve, the mysteries unfold.

Bytes dance and keys whisper secrets untold,
In this digital arena, hearts are bold.
Hackers and thinkers, together they strive,
To conquer the flags, and the glory derive.

In every challenge, knowledge is gained,
In CTF's domain, passions unchained.Key is KPMG{Cryptic_art_unfolded}
```

#### flag : KPMG{Cryptic_art_unfolded}
