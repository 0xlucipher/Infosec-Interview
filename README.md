# Information Security Interview Questions ![GitHub](https://img.shields.io/github/license/0xlucipher/Infosec-Interview.svg?style=popout-square) ![version](https://img.shields.io/badge/version-0.0.1-red.svg?style=popout-square)
collection of interview questions for Information Security domain

## Table of Contents
* [Application Security](#application-security)
* [Encryption](#encryption)
* [Forensics](#forensics)
* [General](#General)
* [Malware](#Malware)
* [Network Forensic](#Network-Forensic)

## Application Security

**Q. If you needed to encrypt and compress data for transmission, which would you do first and why?**

Compress then encrypt. Because encryption takes up resources and can be cumbersome to perform. (If you encrypt first, then compress, then your compression will be useless. Compression doesn't work on random data.) [resource](https://blog.appcanary.com/2016/encrypt-or-compress.html)

**Q. What are the various ways to handle brute forcing?**

* Account Lockouts/timeouts
* API rate limiting
* IP restrictions
* Fail2ban
* ...etc

**Q. What is Cross-Site Request Forgery?**

Cross site request forgery (CSRF), also known as XSRF, Sea Surf or Session Riding, is an attack vector that tricks a web browser into executing an unwanted action in an application to which a user is logged in.
Defense includes but are not limited to:
* check origins header & referer header
* check CSRF tokens or nonce

**Q. What is Cross-Site Scripting? What are the different types of XSS? How to defend against XSS?**

## Encryption 

**Q. What’s the difference between encoding, encryption, hashing and Obfuscation ?**

**Encoding** - The purpose of encoding is to transform data so that it can be properly (and safely) consumed by a different type of system, e.g. binary data being sent over email, or viewing special characters on a web page. The goal is not to keep information secret, but rather to ensure that it’s able to be properly consumed.
Encoding transforms data into another format using a scheme that is publicly available so that it can easily be reversed. It does not require a key as the only thing required to decode it is the algorithm that was used to encode it.

**Encryption** - The purpose of encryption is to transform data in order to keep it secret from others, e.g. sending someone a secret letter that only they should be able to read, or securely sending a password over the Internet. Rather than focusing on usability, the goal is to ensure the data cannot be consumed by anyone other than the intended recipient(s).
Encryption transforms data into another format in such a way that only specific individual(s) can reverse the transformation. It uses a key, which is kept secret, in conjunction with the plaintext and the algorithm, in order to perform the encryption operation. As such, the cipher text, algorithm, and key are all required to return to the plaintext.

**Hashing** - Hashing serves the purpose of ensuring integrity, i.e. making it so that if something is changed you can know that it’s changed. Technically, hashing takes arbitrary input and produce a fixed-length string that has the following attributes:

* The same input will always produce the same output.
* Multiple disparate inputs should not produce the same output.
* It should not be possible to go from the output to the input.
* Any modification of a given input should result in drastic change to the hash.

Hashing is used in conjunction with authentication to produce strong evidence that a given message has not been modified. This is accomplished by taking a given input, hashing it, and then signing the hash with the sender’s private key.

When the recipient opens the message, they can then validate the signature of the hash with the sender’s public key and then hash the message themselves and compare it to the hash that was signed by the sender. If they match it is an unmodified message, sent by the correct person.

**Obfuscation** - The purpose of obfuscation is to make something harder to understand, usually for the purposes of making it more difficult to attack or to copy.
One common use is the the obfuscation of source code so that it’s harder to replicate a given product if it is reverse engineered.

It’s important to note that obfuscation is not a strong control (like properly employed encryption) but rather an obstacle. It, like encoding, can often be reversed by using the same technique that obfuscated it. Other times it is simply a manual process that takes time to work through.

Another key thing to realize about obfuscation is that there is a limitation to how obscure the code can become, depending on the content being obscured. If you are obscuring computer code, for example, the limitation is that the result must still be consumable by the computer or else the application will cease to function.

**Q. How is TLS attacked? How has TLS been attacked in the past? Why was it a problem? How was it fixed?**

* [Weak ciphers](https://www.owasp.org/index.php/Testing_for_Weak_SSL/TLS_Ciphers,_Insufficient_Transport_Layer_Protection_(OTG-CRYPST-001))
* [Heartbleed](http://heartbleed.com/)
* [BEAST](https://blog.qualys.com/ssllabs/2013/09/10/is-beast-still-a-threat)
* [CRIME](https://security.stackexchange.com/questions/19911/crime-how-to-beat-the-beast-successor/19914#19914)
* [POODLE](https://censys.io/blog/poodle)

## Forensics
**Q. What is Chain of custody?**

For legal cases the data/device (evidence) needs to be integrated, hence any access needs to be documented – who, what when and why. Compromise in this process can cause legal issues for the parties involved.

**Q. Define steps of forensic process**

Identification > Collection > preservation > Examination > Analysis > Presentation

**Q. difference in raw/dd image and E01 image**

RAW or DD images just contain the data from the original source, and nothing else. Any hash data etc is usually stored in a separate log file that is generally stored with the image file.

EnCase image format includes a separate hash for each segment, and the hash file and certain information about the image - including information entered by the examiner - is stored inside the image files themselves. Hence an E01 is more than just the image, it also contains metadata relating to the image file.

**Q. Difference in Data recovery and Data carving**

Deleted files are recoverable by using some forensic programs if the deleted file’s space is not overwritten by another file.(file flag has been removed by the os. This kind of file are easier to locate)
 
Data carving is different than data recovery in that data carving searches through raw data on a hard drive without using a file system. Data carving is essential for computer forensics investigators to find data when a hard drive’s data is corrupted. (basically it’s a program that can reconstruct file based on fragments.)

**Q. Types of file carving**

1. Header-footer or header-maximum file size carving, 2. File structure based carving (metadata in the file as well), 3. Content based carving (semantics etc.)[Link](https://users.du.se/~hjo/cs/dt2016/presentation/extra_carving_w4.pdf)

**Q. A user reports that they received a suspicious looking email. How do you proceed?**

Collect the original mail from user or collect the mailbox dump, identify the suspicious mail extract them in eml/msg format (to preserve metadata) extract email header from all the files. And based on email headers (usually taken bottom to top approach process) we can identify original sender (X-originating-IP) and mail server (message-id).
 
important fields are
From, to, Subject, date (time zone difference can be issue) CC, BCC, In-reply-to ID, X-Originating-IP, Received and SMTP server hop details. [Link](https://fenix.tecnico.ulisboa.pt/downloadFile/1970943312267438/csf-13.pdf)

**Q. Explain the difference between a logical, file system and physical extraction of a mobile phone.**

**Q. You are given a phone and asked for all location data relating to Airport. Explain how you would conduct your analysis.**

## General

**Q. Are open source projects more or less secure than proprietary projects?**

The securities of these projects depends mainly on the size of the project, the total number of the developers who are working under this project and the one factor, which is most essential as well as important, is the control of the quality. Just the type of project won’t determine its quality, the inside matter of the corresponding projects will matter.

**Q. What is CIA triangle?**

* Confidentiality: Keeping the information secret.
* Integrity: Keeping the information unaltered.
* Availability: Information is available to the authorized parties at all times.

**Q. What is the difference between threat, vulnerability and risk? give scenario bases example**

threat is what a potential attacker poses, by potentially using a system vulnerability that was never identified as a risk. Using this answer provides context for the three terms together, but you can define them separately.

* A threat is the possibility of an attack.
* A vulnerability is a weakness in the system.
* Risks are items that may cause harm to the system or organization.



## Malware

**Q. What is static analysis?**

**Q. What is dynamic analysis?**

**Q. What type of items do you look for during static analysis?**

**Q. How does static analysis influence how dynamic analysis is performed?**

**Q. Why would you disassemble or debug an application?**

**Q. What is a Windows Portable Executable?**

**Q. How would a piece of malware maintain persistence?**

**Q. What is the ESP register used for in the Intel x86–32 architectures?**


## Network Forensic

**Q. PING work on which port?**

‘ping’ uses ICMP, specifically ICMP echo request and ICMP echo reply packets. There is no ‘port’ associated with ICMP. Ports are associated with the two IP transport layer protocols, TCP and UDP. ICMP packets are identified by the ‘protocol’ field in the IP datagram header.

**Q. Which tool is used for Network forensics?**

**Q. Where you’ll find HTTP referrer Link?**

**Q. What is importance of web user agent?**


## Credits

[Daniel Miessler](https://danielmiessler.com/study/infosec_interview_questions/),[@pbnj](https://github.com/pbnj/infosec-interview-questions), [Jordan Potti](https://jordanpotti.com/2016/12/28/what-to-know-for-your-first-infosec-interview/), [Teckk2](https://teckk2.github.io/misc/2018/01/03/Infosec-Interview_Questions_Part-1.html)
