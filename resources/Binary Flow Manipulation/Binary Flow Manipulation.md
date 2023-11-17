# Binary Flow Manipulation

A notorious organization, "The Enigma Syndicate," has sent encrypted messages detailing a dark conspiracy. Participants must tackle their binary cryptogram using powerful reverse engineering tool to reveal the sinister plot. Unravel the enigma, stop the conspiracy, and become the ultimate codebreaker in this thrilling CTF challenge!

[Payload](/resources/Binary%20Flow%20Manipulation/Payload)

#### Points - 400

## Procedure

Lets start with the usual information gathering, the **file** command:

```Shell
file Payload
```

Output:

```plaintext
Payload: ELF 32-bit LSB executable, Intel 80386, version 1 (GNU/Linux), statically linked, BuildID[sha1]=0ae92b33f8c4df9d7391925f2e24ca5e378d8d0c, for GNU/Linux 3.2.0, with debug_info, not stripped
```

The output tells us that the file is a linux executable, lets execute it:

```Shell
chmod +x payload
./payload
```

The binary basically outputs what input you give to it and exits.

Now, let us employ IDA to work. We see that the main function doesn't do much, all it does is pushes the base pointer onto the stack, it then sets the stack pointer to a 16-byte aligned value and ultimately calls the **ReadInput** function.

![main_codeblock](/resources/Binary%20Flow%20Manipulation/BFM_img1.png)

Okay, so the main function does not give us any idea of where to look for our flag, lets first try skimming though all the function in the binary:

![functions](/resources/Binary%20Flow%20Manipulation/BFM_img2.png)

Here the function that caught my attention was **unreachableFunction** function. Lets have a look at what it does:

![unreachableFunction_codeblock](/resources/Binary%20Flow%20Manipulation/BFM_img3.png)

Bingo! A quick look reveals that some deobfuscation and printing processes are taking place here.

Now how do we access this function? If we recall there is a function call of ReadInput in the main function, all we have to do is replace the function call of **ReadInput** with the function call of **UnreachableFunction** and apply the patch.

![updating_main](/resources/Binary%20Flow%20Manipulation/BFM_img4.png)

Executing the patched binary:

```Shell
./payload_v1
```

Output:

```plaintext
KPMG_CTF{47634f7cdde0d9b804f9d0d603e4cd47}+
```

Patched binary: [patched_binary](/resources/Binary%20Flow%20Manipulation/Patched_Payload)

#### flag : KPMG_CTF{47634f7cdde0d9b804f9d0d603e4cd47}
