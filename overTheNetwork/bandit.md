# Level 0

Connect over ssh 

        ssh username@hostname -p port

![](./sc/sc1.png)

***

&nbsp;

# Level 0 -> Level 1

`ls` to list all the files \
`cat` to read the required file i.e `readme`

![](./sc/sc2.png)

Password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

***

&nbsp;

# Level 1 -> Level 2

![](./sc/sc3.png)

A "dashed" cannot be read by simply providing its name as an argument to cat because `cat -` is used to read from standard input. 
So we have to provide the location of `-` file so that `cat` can interpret it correctly

![](./sc/sc4.png)

We can also use `<`.
`<` redirects the contents of a file to a command

Password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

***

&nbsp;

# Level 2 -> Level 3

If a file has spaces in between its name then we can use inverted commas to enclose the name of the file so that it is interpreted correctly 

![](./sc/sc5.png)

Password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
***

&nbsp;

# Level 3 -> Level 4

`ls -a` lists all the files including the hidden ones

![](./sc/sc6.png)

Password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

***

&nbsp;

# Level 4 -> Level 5

`file` command can be used to list files along with their type

![](./sc/sc7.png)

Password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

***

&nbsp;

# Level 5 -> Level 6

`find` command can be used to find files
`-type f` specifies that it is a file and not a directory
`-size 1033c` specifies that size of file is 1033 bytes
`! -executable` specifies that is not an executable

![](./sc/sc8.png)

Password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

***

&nbsp;

# Level 6 -> Level 7

Every file belongs to a user and a group
We can see that by using `ls -l` command

We can find files belonging to a user or a group by appending `-group grp_nm` and `-user usr_nm` to the `find` command.

`2> /dev/null` redirects all the ouput on stderr channel to `/dev/null/` so that the error is not printed in the terminal
The error is this case is `permission denied` as `find` does not have permission to look into some directories

![](./sc/sc9.png)

Password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

***

&nbsp;

# Level 7 -> Level 8

Since the `data.txt` contains many lines, it becomes difficult to find the word "millionth" just scrolling through it. So we use `|` pipe operator to `grep` or "grab" the line that contains the "millionth". \
The `|` operator connects the stdout of whatevers on the left of it to stdin of whatevers on the right of it.

![](./sc/sc10.png)

Password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

***

&nbsp;

# Level 8 -> Level 9

To find unique lines we can use `uniq -u` command but this command only filters out those lines that are same but one after the other. So in order to find the line that occurs only once first we have to sort it.

![](./sc/sc11.png)

Password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

***

&nbsp;

# Level 9 -> Level 10

Since `data.txt` contains binary, we cannot read it with just cat. \
`strings` command can be used to extract text from a binary file. \
Finally `grep`ing the lines that contains "=====" gives us the flag.

![](./sc/sc12.png)

Password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

***

&nbsp;

# Level 10 -> Level 11

The `data.txt` file contains bas64 encoded data. \
So we will use `base64 -d` command to decode it.\
the `<` characters redirectos `data.txt`'s contents to base64 as an argument.

![](./sc/sc13.png)

Password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
***

&nbsp;

# Level 11 -> Level 12

The `tr` command can be used to replace characters. \
The first argument is the set of characters that are being replaced and the second argument is the set of characters that are replacing. \
Since this is Rot13, a is replaced by n and so on.

![](./sc/sc14.png)

Password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

***

&nbsp;

# Level 12 -> Level 13

We use `mktemp` to create a temporary directory and move into it. \
Then we use `cp` to copy the contents of `~data.txt` to copy the contents into our temporary directory \
Now we have to find out what kind of file is data.txt.
Since data.txt is an ASCII file we have to convert it to binary \
`xxd -r ./data.txt ./binary` converts hex-dump of data.txt into binary \
`file binary` tells us that it is a gzip compressed data \
so we copy the contents of of `binary` into a file with extension `gz` \
Then we use `gzip -d` to decompress the contents \
Then we use `file` again to check the file type \
Then repeat the process untill we get a human readable format.

         
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cat binary
        ���fdata2.bin>��BZh91AY&SYʃ������������������ݿ~[���߾��o������;V4�i���CF�CA����i��hѠ�3Q���QFF�4� �&MF������d4���O���4шC�
        �d�F��hɦ�0�hh�2*�`Q��S/                                                                                                @i�&F��@�@4i��h�
                        ���]�N��')!L��L�5��O�Z
        �=g!Wb^
        �d     �����#�{B��9�v�/tJ���<N�7o�#E�_#
        54�)A����
                tOJQ��#�̜�匔a���JB�a�}6�"�YⵟQ���*��0h���}�����|��!	&��n�"��{�
                                                                                �Go7
                                                                                6a�ީ�/�F��8��S6��Gα�S7�H1R�A��&�l(�$��e�\�l�ن�"G�ՋX�Vz�
                                                                                                                                        ���\c�%	a,Sd�}$���`�Ǿ
        ��G�Cp���C�ˈ*J�K���g��g����#mAj(��`��.R)}��N0��&F�]0b&(�N�KgT8�BJ���.Ƀ���]��BC*�Y>bandit12@bandit:/tmp/tmp.OyanraRlRI$ 
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file binary
        binary: gzip compressed data, was "data2.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 574
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ mv binary data2.gz
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2.gz  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ gzip -d data2.gz
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cat data2
        BZh91AY&SYʃ������������������ݿ~[���߾��o������;V4�i���CF�CA����i��hѠ�3Q���QFF�4� �&MF������d4���O���4шC�
        �d�F��hɦ�0�hh�2*�`Q��S/                                                                                @i�&F��@�@4i��h�
                        ���]�N��')!L��L�5��O�Z
        �=g!Wb^
        �d     �����#�{B��9�v�/tJ���<N�7o�#E�_#
        54�)A����
                tOJQ��#�̜�匔a���JB�a�}6�"�YⵟQ���*��0h���}�����|��!	&��n�"��{�
                                                                                �Go7
                                                                                6a�ީ�/�F��8��S6��Gα�S7�H1R�A��&�l(�$��e�\�l�ن�"G�ՋX�Vz�
                                                                                                                                        ���\c�%	a,Sd�}$���`�Ǿ
        ��G�Cp���C�ˈ*J�K���g��g����#mAj(��`��.R)}��N0��&F�]0b&(�N�KgT8�BJ���.Ƀ���]��BC*�bandit12@bandit:/tmp/tmp.OyanraRlRI$ 
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data2
        data2: bzip2 compressed data, block size = 900k
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ man bzip2
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cp data2 data3.bz2
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3.bz2  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ bzip2 -d data3.bz2
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data3
        data3: gzip compressed data, was "data4.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 20480
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cp data3 data4.gz
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4.gz  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ gzip -d data4.gz
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data4
        data4: POSIX tar archive (GNU)
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ man tar
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cp data4 data5.tar
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ man tar
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ tar -x data5.tar
        tar: Refusing to read archive contents from terminal (missing -f option?)
        tar: Error is not recoverable: exiting now
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ tar -xf data5.tar
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data5.bin  data5.tar  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data5.bin
        data5.bin: POSIX tar archive (GNU)
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ tar -xf data5.bin
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data5.bin  data5.tar  data6.bin  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data6.bin
        data6.bin: bzip2 compressed data, block size = 900k
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cp data6.bin data7.bz2
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ bzip2 -d data7.bz2 
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data5.bin  data5.tar  data6.bin  data7  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data7
        data7: POSIX tar archive (GNU)
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cp data7 ./data8.tar
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ tar -xf data8.tar
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data5.bin  data5.tar  data6.bin  data7  data8.bin  data8.tar  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data8.bin
        data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 49
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cp data8.bin ./data9.gz
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data5.bin  data5.tar  data6.bin  data7  data8.bin  data8.tar  data9.gz  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ gzip -d data9.gz
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ ls
        data2  data3  data4  data5.bin  data5.tar  data6.bin  data7  data8.bin  data8.tar  data9  data.txt
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ file data9
        data9: ASCII text
        bandit12@bandit:/tmp/tmp.OyanraRlRI$ cat data9
        The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
        bandit12@bandit:
The password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

***

&nbsp;

# Level 13 -> Level 14

Establish an ssh connection to `bandit14`
The client initiates the transmission control protocol (TCP) handshake negotiating the secure connection, verifying the servers identity and providing credentials for authentication \
After the TCP connection is established the server shares its public host key which the client can use to identify the host. \
Now both parties negotiate a session key using a version of something called the Diffie-Hellman algorithm. This algorithm (and its variants) make it possible for each party to combine their own private data with public data from the other system to arrive at an identical secret session key.

        ssh -i ./sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

Then read the password

        
        bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
        MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

***

&nbsp;

# Level 14 -> Level 15

Telnet can be used to connect to localhost. \
Before `ssh`, telnet was used to connect to remote shell but it was unsecure which means anyone could sniff the packets flowing through telnet protocol \
Since we are connecting to localhost's port (Ports are vitual points where network communication happenn. These ports are managed by the operating system) 30000 we can use telnet. \

![](./sc/sc15.png)

The password: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

***

&nbsp;

# Level 15 -> Level 16
The Secure Socket Layer (SSL) is a cryptographic protocol designed to provide secure communication over a computer network \
The Transport Layer Security (TLS) is the successor to SSL and is designed to provide improved security and efficiency. TLS was developed as an enhancement of SSL to the address various vulnerabilities and to the incorporate modern cryptographic techniques\
OpenSSL is an all-around cryptography library that offers an open-source application of the TLS protocol.

The flag `s_client` specified `TLS` encryption technique when connecting.

    bandit15@bandit:~$ openssl s_client -connect localhost:30001

    
    ---
    read R BLOCK
    8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
    Correct!
    kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

    closed

***

&nbsp;

# Level 16 -> Level 17
The list of ports that are open on localhost \
`nmap -sV localhost -p 31000-32000`
    
    bandit16@bandit:~$ nmap -sV localhost -p 31000-32000
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-18 13:38 UTC
    Stats: 0:00:27 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
    Service scan Timing: About 0.00% done
    Stats: 0:01:23 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
    Service scan Timing: About 80.00% done; ETC: 13:39 (0:00:21 remaining)
    Stats: 0:02:16 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
    Service scan Timing: About 80.00% done; ETC: 13:40 (0:00:34 remaining)
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00019s latency).
    Not shown: 996 closed tcp ports (conn-refused)
    PORT      STATE SERVICE     VERSION
    31046/tcp open  echo
    31518/tcp open  ssl/echo
    31691/tcp open  echo
    31790/tcp open  ssl/unknown
    31960/tcp open  echo

As we can se here there are two ports 31518 and 31790 that speaks ssl but 31518 echos back so correct port is 31790. \
Now we connect to that port and provide the password


    bandit16@bandit:~$ ncat --ssl localhost 31790
    kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
    Correct!
    -----BEGIN RSA PRIVATE KEY-----
    MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ

(I dont know why openssl was not working, when i entered the password it returned keyupdate)

Now we save this private key into a file and use it to `ssh` into bandit17

    bandit16@bandit:/tmp$ ssh -i pvt.key bandit17@localhost -p 2220

***

&nbsp;

# Level 17 -> Level 18

    
    bandit17@bandit:~$ diff passwords.new passwords.old
    42c42
    < x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
    ---
    > ktfgBvpMzWKR5ENj26IbLGSblgUG9CzB
    bandit17@bandit:~$ 

