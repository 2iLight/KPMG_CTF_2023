
# Binary Cryptogram - unravel the enigma

A notorious organization, "The Enigma Syndicate," has sent encrypted messages detailing a dark conspiracy. Participants must tackle their binary cryptogram using powerful reverse engineering tool to reveal the sinister plot. Unravel the enigma, stop the conspiracy, and become the ultimate codebreaker in this thrilling CTF challenge!

[Payload](/resources/Binary%20Cryptogram%20-%20unravel%20the%20enigma/Enigma_Binary)

#### Points - 250

## Procedure

Firstly, we will gather info about the binary Payload, we'll start with **file** command:

```Shell
file Payload
```

The output tells us that the given payload is a linux binary executable, let's try executing it:

```Shell
$ chmod +x payload
$ ./payload
```

Output:

```plaintext
Not_so_easy 
```

After conducting initial static analysis techniques, such as exploring hex dumps and strings, we have not made significant progress. To proceed further, it's time to employ more advanced tools like IDA.

The graph view in IDA comprises several code blocks, delineated by conditional statements. When organized correctly, these blocks can trigger the printing of the flag.

## Attempt 1 :

![main_derivations](/resources/Binary%20Cryptogram%20-%20unravel%20the%20enigma/attempt1_1.png)

The conditional operation in first code block results in control flow to code block at memory location in **loc_13E5** which in turn prints "Not_so_easy" and ends the execution leaving other code bocks unexecuted. We need to alter this flow:

![alter_main_derivations](/resources/Binary%20Cryptogram%20-%20unravel%20the%20enigma/attempt1_3.png)

We achieved this alteration by replacing the previous address of **loc_13E5** with **loc_11FE** in the first code block using the assemble instruction option in IDA. Now let's apply the patch and execute the binary:

```plaintext
zsh: segmentation fault  ./Enigma_Binary
```

At first you might think that the patch has broken the binary, this can however be proven wrong.
The pseudocode of the code block at **loc_11FE** clearly shows that it is meant to cause an error.

```assembly
if ( argc > 1 )
  {
    __outdword(1u, v3);
    JUMPOUT(0x11FCLL);
  }
```

## Attempt 2

![Final_patch](/resources/Binary%20Cryptogram%20-%20unravel%20the%20enigma/attempt2_1.png)

In this version of the patch we will skip the code block causing error and use the **jmp** assembly instruction to jump the control flow of the program to the code block at **loc_1126**. having a look at the disassembly, this code block leads to another code block with the statement:

```c
printf("Decrypted Flag: %s\n");
```

This is a good sign. Now lets apply the patch and execute the binary:

```plaintext
Decrypted Flag: KPMG_CTF{be441ba8020e7ea99cd879b156db1e79}
```

patched binary: [patched_payload](/resources/Binary%20Cryptogram%20-%20unravel%20the%20enigma/Enigma_Binary_patched)

#### flag: KPMG_CTF{be441ba8020e7ea99cd879b156db1e79}
