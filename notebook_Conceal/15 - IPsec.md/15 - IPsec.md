# 15 - IPsec


# ike-scan

```bash
┌─[user@parrot]─[10.10.14.9]─[~/htb/conceal/ike-scan]
└──╼ $ sudo ike-scan 10.10.10.116  -M
Starting ike-scan 1.9.4 with 1 hosts (http://www.nta-monitor.com/tools/ike-scan/)
10.10.10.116    Main Mode Handshake returned
        HDR=(CKY-R=51b514c83957e444)
        SA=(Enc=3DES Hash=SHA1 Group=2:modp1024 Auth=PSK LifeType=Seconds LifeDuration(4)=0x00007080)
        VID=1e2b516905991c7d7c96fcbfb587e46100000009 (Windows-8)
        VID=4a131c81070358455c5728f20e95452f (RFC 3947 NAT-T)
        VID=90cb80913ebb696e086381b5ec427b1f (draft-ietf-ipsec-nat-t-ike-02\n)
        VID=4048b7d56ebce88525e7de7f00d6c2d3 (IKE Fragmentation)
        VID=fb1de3cdf341b7ea16b7e5be0855f120 (MS-Negotiation Discovery Capable)
        VID=e3a5966a76379fe707228231e5ce8652 (IKE CGA version 1)

Ending ike-scan 1.9.4: 1 hosts scanned in 0.073 seconds (13.63 hosts/sec).  1 returned handshake; 0 returned notify
```

`
SA=(Enc=3DES Hash=SHA1 Group=2:modp1024 Auth=PSK LifeType=Seconds LifeDuration(4)=0x00007080)
`
This part is important for ipsec configuration.



# ipsec.secrets
```
┌─[user@parrot]─[10.10.14.9]─[~/htb/conceal]
└──╼ $ sudo cat /etc/ipsec.secrets 
# This file holds shared secrets or RSA private keys for authentication.

# RSA private key for this host, authenticating it to any other host
# which knows the public part.


10.10.10.116 %any : PSK "Dudecake1!"
```

# ipsec.conf
```
┌─[user@parrot]─[10.10.14.9]─[~/htb/conceal]
└──╼ $ sudo grep -v "#" /etc/ipsec.conf 
config setup
conn Conceal
      type=transport
      keyexchange=ikev1
      left=10.10.14.9
      leftprotoport=tcp
      right=10.10.10.116
      rightprotoport=tcp
      authby=psk
      esp=3des-sha1
      ike=3des-sha1-modp1024
      ikelifetime=8h
      auto=start
```

This ipsec vpn configuration will create a client-to-site connection.

# Connect to the VPN

```
┌─[user@parrot]─[10.10.14.9]─[~/htb/conceal]
└──╼ $ sudo ipsec start --nofork
[sudo] password for user:
Starting strongSwan 5.9.1 IPsec [starter]...
00[DMN] Starting IKE charon daemon (strongSwan 5.9.1, Linux 5.10.0-6parrot1-amd64, x86_64)
00[CFG] loading ca certificates from '/etc/ipsec.d/cacerts'
00[CFG] loading aa certificates from '/etc/ipsec.d/aacerts'
00[CFG] loading ocsp signer certificates from '/etc/ipsec.d/ocspcerts'
00[CFG] loading attribute certificates from '/etc/ipsec.d/acerts'
00[CFG] loading crls from '/etc/ipsec.d/crls'
00[CFG] loading secrets from '/etc/ipsec.secrets'
00[CFG]   loaded IKE secret for 10.10.10.116 %any
00[LIB] loaded plugins: charon aesni aes rc2 sha2 sha1 md5 mgf1 random nonce x509 revocation constraints pubkey pkcs1 pkcs7 pkcs8 pkcs12 pgp dnskey sshkey pem openssl fips-prf gmp agent xcbc hmac gcm drbg attr kernel-netlink resolve socket-default connmark stroke updown eap-mschapv2 xauth-generic counters
00[LIB] dropped capabilities, running as uid 0, gid 0
00[JOB] spawning 16 worker threads
charon (12789) started after 20 ms
06[CFG] received stroke: add connection 'Conceal'
06[CFG] added configuration 'Conceal'
07[CFG] received stroke: initiate 'Conceal'
07[IKE] initiating Main Mode IKE_SA Conceal[1] to 10.10.10.116
07[ENC] generating ID_PROT request 0 [ SA V V V V V ]
07[NET] sending packet: from 10.10.14.9[500] to 10.10.10.116[500] (236 bytes)
09[NET] received packet: from 10.10.10.116[500] to 10.10.14.9[500] (208 bytes)
09[ENC] parsed ID_PROT response 0 [ SA V V V V V V ]
09[IKE] received MS NT5 ISAKMPOAKLEY vendor ID
09[IKE] received NAT-T (RFC 3947) vendor ID
09[IKE] received draft-ietf-ipsec-nat-t-ike-02\n vendor ID
09[IKE] received FRAGMENTATION vendor ID
09[ENC] received unknown vendor ID: fb:1d:e3:cd:f3:41:b7:ea:16:b7:e5:be:08:55:f1:20
09[ENC] received unknown vendor ID: e3:a5:96:6a:76:37:9f:e7:07:22:82:31:e5:ce:86:52
09[CFG] selected proposal: IKE:3DES_CBC/HMAC_SHA1_96/PRF_HMAC_SHA1/MODP_1024
09[ENC] generating ID_PROT request 0 [ KE No NAT-D NAT-D ]
09[NET] sending packet: from 10.10.14.9[500] to 10.10.10.116[500] (244 bytes)
10[NET] received packet: from 10.10.10.116[500] to 10.10.14.9[500] (260 bytes)
10[ENC] parsed ID_PROT response 0 [ KE No NAT-D NAT-D ]
10[ENC] generating ID_PROT request 0 [ ID HASH N(INITIAL_CONTACT) ]
10[NET] sending packet: from 10.10.14.9[500] to 10.10.10.116[500] (100 bytes)
11[NET] received packet: from 10.10.10.116[500] to 10.10.14.9[500] (68 bytes)
11[ENC] parsed ID_PROT response 0 [ ID HASH ]
11[IKE] IKE_SA Conceal[1] established between 10.10.14.9[10.10.14.9]...10.10.10.116[10.10.10.116]
11[IKE] scheduling reauthentication in 28173s
11[IKE] maximum IKE_SA lifetime 28713s
11[ENC] generating QUICK_MODE request 1984467952 [ HASH SA No ID ID ]
11[NET] sending packet: from 10.10.14.9[500] to 10.10.10.116[500] (220 bytes)
12[NET] received packet: from 10.10.10.116[500] to 10.10.14.9[500] (188 bytes)
12[ENC] parsed QUICK_MODE response 1984467952 [ HASH SA No ID ID ]
12[CFG] selected proposal: ESP:3DES_CBC/HMAC_SHA1_96/NO_EXT_SEQ
12[IKE] CHILD_SA Conceal{1} established with SPIs ce826b18_i 12e6658c_o and TS 10.10.14.9/32[tcp] === 10.10.10.116/32[tcp]
12[ENC] generating QUICK_MODE request 1984467952 [ HASH ]
12[NET] sending packet: from 10.10.14.9[500] to 10.10.10.116[500] (60 bytes)
13[NET] received packet: from 10.10.10.116[500] to 10.10.14.9[500] (76 bytes)
13[ENC] parsed QUICK_MODE response 1984467952 [ HASH N(INIT_CONTACT) ]
13[IKE] ignoring fourth Quick Mode message
```