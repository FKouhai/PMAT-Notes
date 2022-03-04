# Basic Static Analysis
- Definition -> Basic triage approach without detonating the malware
- First step
	- unzip the malware
	- open a terminal and get the sha256 of the malware sample and an md5sum of the malware
	- search on [virus total](https://virustotal.com) the fingerprint we got of the malware
	- using strings of floss to get the possible strings of the binary i.e like a malicious url
	- use a program like pe view to view the malware and extract more data
	- A portable file always starts with MZ
	-  A good thing to check may be the virtual size and the raw data size, the virtual size of the exe file is the data in bytes that the executable will use, and the raw data size is the size in bytes that the binary uses without being run, if the virtual size is way bigger than the raw data that usually means that it is packed binary
			 ![[Pasted image 20211212100217.png]]
	- [Windows API](WindowsAPI.md)
	- The import address table is a table that contains the API calls in a program

		![[Pasted image 20211212112220.png]]
		
		