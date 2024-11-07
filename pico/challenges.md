# Vigenere

1. Objective: Decipher the text 

The Vigenere cipher is a method of encrypting alphabetic text where each letter of the plaintext is encoded with a different Caesar cipher, whose increment is determined by the corresponding letter of another text, the key. 

The encoded text is `rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_cc82272b}` \
The key is `CYLAB` 

The decryption process works like this \
The first letter `r` will be shifted by 2 positions in the alphabet because the first letter in the key `C` whose postion in alphabets is 2. \
Similarly all the letters will be shifted accordingly. \
The numeric position of the letters in the key gives the increment of the corresponding letter in the encoded text. 

The flag is `picoctf{d0nt_us3_v1g3n3r3_c1ph3r_ae82272q}`

&nbsp;

***

# Easy 1

1. Objective: Use the table given to decipher the text `UFJKXQZQUNB` using the key `SOLVECRYPTO`

The table is a 26*26 matrix of letters where each rows first letter is the corresponding letter at that index in the alphabet. \
2nd rows first letter is B, 3rd rows first letter is C and so on. \
Same of columns also 

We can solve this manually by placing the KEY on the column and finding the corresponding letter from the text in that column
and taking taking the value of the row.
The value of the row is the decrypted letter.

Other method is that this is encoded with Vignere cipher. 

The flag is `picoCTF{CRYPTOISFUN}`

&nbsp;

***

# Corewars

1. Objective: Loose from a corewars oponent

Since the oponent is an imp which means it only replicates itself by moving ahead in the memory one step at a time, it will eventually destroy our core if we do not stop it.\
So our player in this case has no instruction. 

```Red
    ;redcode
    ;name myWarrior
    ;assert 1
    end
```

    
    ❯ nc saturn.picoctf.net 61400 < my.red
    ;redcode
    ;name myWarrior
    ;assert 1
    mov 0,3
    end
    Submit your warrior: (enter 'end' when done)

    Warrior1:
    ;redcode
    ;name myWarrior
    ;assert 1
    mov 0,3
    end

    Rounds: 100
    Warrior 1 wins: 0
    Warrior 2 wins: 100
    Ties: 0
    You did it!
    picoCTF{h3r0_t0_z3r0_4m1r1gh7_f1e207c4}

&nbsp;

***

# Verify

Checksums are values derived from a data set to help verify the integrity of that data. They are generally used to detect errors in data during transmission or storage.

A checksum for a data will be same each time it is generated. 

The checksum of the flag file is already givem so we just have to generate checksums of all the files in the `files` directory and match it with the given checksum and that will give us the right file. 

        
    ctf-player@pico-chall$ sha256sum files/* | grep -f checksum.txt    
    5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda  files/8eee7195
    ctf-player@pico-chall$ ./decrypt.sh files/8eee7195
    picoCTF{trust_but_verify_8eee7195}

&nbsp;

***

# Mob psycho
