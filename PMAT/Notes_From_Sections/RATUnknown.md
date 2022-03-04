# RAT Unknown

## Basic Static Analysis

After running floss and pe view it looks like its a piece of software written in nim and compiled in mingw

![[Pasted image 20211214212749.png]]
![[Pasted image 20211214222426.png]]

It also looks like its trying to run an encrypted connection somewhere, or its trying to act as a server for a remote connection

![[Pasted image 20211214213039.png]]
![[Pasted image 20211214214024.png]]

By running pe view we determine this malware at first doesnt look like a packed binary, but its pretty small in size

![[Pasted image 20211214213340.png]]

we were also able to determine that this malware is a portable exe

![[Pasted image 20211214213837.png]]



By running pestudio we were able to get the hash sums

- md5 -> 689FF2C6F94E31ABBA1DDEBF68BE810E
- sha1 -> 69B8ECF6B7CDE185DAED76D66100B6A31FD1A668
- ```sha ->256248D491F89A10EC3289EC4CA448B19384464329C442BAC395F680C4F3A345C8C```

### VT analysis
Virus total was unable to find the fingerprint

We were also able to determine that this program uses the following libraries

![[Pasted image 20211214213933.png]]

Which are usually used for malicious intends

In pestudio we were also able to see that it contains the following string

![[Pasted image 20211214214134.png]]

Which could be related to TLS

## Basic Dynamic analysis

Once running the malware, we notice that it tries to ping the ubuntu ntp server
![[Pasted image 20211214214956.png]]

Possible hit

![[Pasted image 20211214215106.png]]

It looks like the malware is trying to access an aws ec2 instance that is running ubuntu, and its trying to download msdcorelib.exe to execute it
![[Pasted image 20211214215443.png]]
![[Pasted image 20211214215658.png]]

The malware also attempts to do a buffer overflow, possibly by dividing by zero some numbers, it looks like its trying to query a lot of registry keys in order to accomplish the buffer overflow

![[Pasted image 20211214215603.png]]

After running tcpview on the infected machine we noticed that the malware sets up a listening connection on port 5555

![[Pasted image 20211215212610.png]]

From remnux we run netcat to connect to the host on that port and we see a bas64 greeter

![[Pasted image 20211215212819.png]]

We see that indeed it is a remote shell

![[Pasted image 20211215212919.png]]

And that it transfers the information to the client encoding it into base64

## Conclusions

After the RATUnknown trying to hit that ec2 intance(probably its c2), it attempts to download an exe file msdcorelib.exe this file its very likely to establish a remote connection back to the c2 hq