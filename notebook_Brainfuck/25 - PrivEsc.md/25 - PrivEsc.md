# 25 - PrivEsc

# Files in user's home directory
```bash
orestis@brainfuck:~$ ls -l 
total 20
-rw------- 1 orestis orestis  619 Apr 29  2017 debug.txt
-rw-rw-r-- 1 orestis orestis  580 Apr 29  2017 encrypt.sage
drwx------ 3 orestis orestis 4096 Apr 29  2017 mail
-rw------- 1 orestis orestis  329 Apr 29  2017 output.txt
-r-------- 1 orestis orestis   33 Apr 29  2017 user.txt
```

# debug.txt

```
7493025776465062819629921475535241674460826792785520881387158343265274170009282504884941039852933109163193651830303308312565580445669284847225535166520307
7020854527787566735458858381555452648322845008266612906844847937070333480373963284146649074252278753696897245898433245929775591091774274652021374143174079
30802007917952508422792869021689193927485016332713622527025219105154254472344627284947779726280995431947454292782426313255523137610532323813714483639434257536830062768286377920010841850346837238015571464755074669373110411870331706974573498912126641409821855678581804467608824177508976254759319210955977053997
```

#  output.txt 
```
Encrypted Password: 44641914821074071930297814589851746700593470770417111804648920018396305246956127337150936081144106405284134845851392541080862652386840869768622438038690803472550278042463029816028777378141217023336710545449512973950591755053735796799773369044083673911035030605581144977552865771395578778515514288930832915182
```

# encrypt.sage 
```
nbits = 1024

password = open("/root/root.txt").read().strip()
enc_pass = open("output.txt","w")
debug = open("debug.txt","w")
m = Integer(int(password.encode('hex'),16))

p = random_prime(2^floor(nbits/2)-1, lbound=2^floor(nbits/2-1), proof=False)
q = random_prime(2^floor(nbits/2)-1, lbound=2^floor(nbits/2-1), proof=False)
n = p*q
phi = (p-1)*(q-1)
e = ZZ.random_element(phi)
while gcd(e, phi) != 1:
    e = ZZ.random_element(phi)



c = pow(m, e, n)
enc_pass.write('Encrypted Password: '+str(c)+'\n')
debug.write(str(p)+'\n')
debug.write(str(q)+'\n')
debug.write(str(e)+'\n')
```
This line here *random_prime(2^floor(nbits/2)-1, lbound=2^floor(nbits/2-1), proof=False)* is interesting and we should google it.

[ctftime](https://ctftime.org/writeup/6434) has almost the identical code, it says **It is a standard RSA with e=5 and 1024 bits modulus. What is noticable is that we get 5 payloads, and e is 5, so the setup looks very much like for a Hastad Broadcast Attack. Also the name of the task could suggest this. **

It is RSA

This is from [Wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
```
In a public-key cryptosystem, the encryption key is public and distinct from the decryption key, which is kept secret (private). An RSA user creates and publishes a public key based on two large prime numbers, along with an auxiliary value. The prime numbers are kept secret. Messages can be encrypted by anyone, via the public key, but can only be decoded by someone who knows the prime numbers.
```

Luckly, we already know the prime numbers, now we should google  **crack rsa given p q and e**

# Python code
https://crypto.stackexchange.com/questions/19444/rsa-given-q-p-and-e 


```py
import math

def getModInverse(a, m):
    if math.gcd(a, m) != 1:
        return None
    u1, u2, u3 = 1, 0, a
    v1, v2, v3 = 0, 1, m

    while v3 != 0:
        q = u3 // v3
        v1, v2, v3, u1, u2, u3 = (
            u1 - q * v1), (u2 - q * v2), (u3 - q * v3), v1, v2, v3
    return u1 % m

def main():
    # p, prime number, the first line from debug.txt
    p = 7493025776465062819629921475535241674460826792785520881387158343265274170009282504884941039852933109163193651830303308312565580445669284847225535166520307 
    # q, prime number, the second line
    q = 7020854527787566735458858381555452648322845008266612906844847937070333480373963284146649074252278753696897245898433245929775591091774274652021374143174079 
    # output.txt & /root/root.txt
    ct = 44641914821074071930297814589851746700593470770417111804648920018396305246956127337150936081144106405284134845851392541080862652386840869768622438038690803472550278042463029816028777378141217023336710545449512973950591755053735796799773369044083673911035030605581144977552865771395578778515514288930832915182 
    # e, the third line from debug.txt
    e = 30802007917952508422792869021689193927485016332713622527025219105154254472344627284947779726280995431947454292782426313255523137610532323813714483639434257536830062768286377920010841850346837238015571464755074669373110411870331706974573498912126641409821855678581804467608824177508976254759319210955977053997 
    n = p*q

    # compute n
    n = p * q

    # Compute phi(n)
    phi = (p - 1) * (q - 1)

    # Compute modular inverse of e
    d = getModInverse(e, phi)

    print("n:  " + str(d))

    # Decrypt ciphertext
    pt = pow(ct, d, n)
    print("pt: " + str(pt))

if __name__ == "__main__":
    main()
```

# Let's run the script
```
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/brainfuck/exploit]
└─$ python3 decrypt.py 
n:  8730619434505424202695243393110875299824837916005183495711605871599704226978295096241357277709197601637267370957300267235576794588910779384003565449171336685547398771618018696647404657266705536859125227436228202269747809884438885837599321762997276849457397006548009824608365446626232570922018165610149151977
pt: 24604052029401386049980296953784287079059245867880966944246662849341507003750
```

pt: should be the plain text as number, the easiest way to turn it back would be converting from integer to hex and then hex to str.

```py
$ python3
>>> hex(24604052029401386049980296953784287079059245867880966944246662849341507003750)
'0x3665666331613564626238393034373531636536353636613330356262386566' # 0x part needs to be removed for the next method.
>>> bytearray.fromhex('3665666331613564626238393034373531636536353636613330356262386566').decode()    # /root/root.txt                                                                                
```
