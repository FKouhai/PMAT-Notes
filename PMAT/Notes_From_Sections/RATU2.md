# RAT UNKNOWN 2
## Basic Static Analysis

### Hashes
md5 -> EE40C2C8BFF8D5855DE5B3A41794BDE8
sha1 -> 93D41836B3B253E2532E14015435AAFC5D88DBB7
sha256 -> 8501517654671974F1DC8875BCE4217CEE8ECF4DB4D2ED45AE3BC4CF0BA96DAE

---

After opening peview, we see that this malware is a portable executable

![[Pasted image 20211219121642.png]]

We can also see that this binary isnt a packed one, by checking the data raw size and virtual size

![[Pasted image 20211219121812.png]]


By running FLOSS, we see that this is a binary compiled in nim

![[Pasted image 20211219122024.png]]

We can also see that this binary when run tries to open a socket, and also creates a file

![[Pasted image 20211219122139.png]]
![[Pasted image 20211219122244.png]]

We can also see that this binary invokes a command in cmd

![[Pasted image 20211219122338.png]]

After running pestudio on the binary, we can see that there are a few functions that could be potentially used for malware development

![[Pasted image 20211219122611.png]]

There are also some strings that are usually used in malware development

![[Pasted image 20211219122710.png]]

## Basic Dynamic Analysis

After opening wireshark on our remnux host and arming the malware, we see that this binary tries to run an nslookup on

aaaaaaaaaaaaaaaaaaaa.kadusus.local

We see in the packet capture, the following

![[Pasted image 20211219123814.png]]

After firing up procmon, we see that the binary tries to connect via https to the domain name found earlier

![[Pasted image 20211219124807.png]]

After running netcat listening on port 443, we see the following output

![[Pasted image 20211219124953.png]]

It looks that the malware tries to connect via 443 to the remote host and serves up a remote shell, sort of what we saw in [RAT UNKNOWN](RATUnknown)

As an addition, we can see in procmon the process tree

![[Pasted image 20211219130639.png]]

## Conclusions
After the analysis on this binary, we can conclude that this malware has a reverse shell capability, allowing an attacket to run commands remotely on the infected machine, it could also be used for pivoting and lateral movement at an organization