# SillyPutty

- What is the SHA256 hash of the sample 
   BBEC96F83A7EBFE16114934DAB38B796AE296BFCC8FF6C8BC97511F872DEC86D
- What architecture is this binary?
	x86 Windows executable

- Are there any results from submitting the SHA256 hash to VirusTotal??
	No

- Describe the results of pulling the strings from this binary. Record and describe any strings that are potentially interesting. Can any interesting information be extracted from the strings?
	ascii,12,0x000A6E27,-,file,winspool.drv
	![[Pasted image 20211219153946.png]]
	![[Pasted image 20211219154025.png]]
	![[Pasted image 20211219154046.png]]
	![[Pasted image 20211219154101.png]]

- Describe the results of inspecting the IAT for this binary. Are there any imports worth noting?
	
![[Pasted image 20211219154214.png]]
![[Pasted image 20211219154225.png]]

- Is it likely that this binary is packed?
	No, this is not a packed binary, since the virtual size and the raw data sice are similar
	![[Pasted image 20211219154312.png]]
---
 - Describe initial detonation. Are there any notable occurances at first detonation? Without internet simulation? With internet simulation?
	On Procmon we are able to see that putty spawns a powershell command and conhost.exe
	![[Pasted image 20211219154821.png]]
	
 - From the host-based indicators perspective, what is the main payload that is initiated at detonation? What tool can you use to identify this?
 	powershell.exe
	conhost.exe
	procmon can be used for identifying this

 - What is the DNS record that is queried at detonation?
	bonus2.corporatebonusapplication.local

 - What is the callback port number at detonation?
	8443

 - What is the callback protocol at detonation?
	HTTP

 - How can you use host-based telemetry to identify the DNS record, port, and protocol?
		By using procmon and icnluding a filter for TCP in Operation contains

 - Attempt to get the binary to initiate a shell on the localhost. Does a shell spawn? What is needed for a shell to spawn?
	 ![[Pasted image 20211219155745.png]]
	 The way to spawn a shell is by having a proper TLS connection, if not we wont be able to get a shell 
 	


## Basic Static Analysis
Running pestudio, we find the following functions, which are likely to be 

## Basic Dynamic Analysis

## Conclusions
