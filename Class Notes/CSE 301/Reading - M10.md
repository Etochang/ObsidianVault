202406111854
Meta Tags: #class
Tags: [[ethics]]

# Reading - M10

>Chapter 7

## 7-1 Introduction

Millions of people and most businesses rely upon computers and the Internet to conduct their affairs, making the security of these systems an important issue.

## 7-2 Hacking

### Hackers, Past and Present

In its original meaning, a **hacker** was an explorer, a risk taker, someone who was trying to make a system do something it had never done before. Calling someone a hacker was a sign of respect; hackers wore the label with pride.

In 1959, some of the original hackers shifted their attention to electronic computers. The term "hacker" came to mean a "person who delights in having an intimate understanding of the internal workings of a system, computers, and networks in particular."

In the 1983 movie *WarGames*, a teenager breaks into a military computer and nearly causes a nuclear Armageddon. This inspired a lot of teenagers to become highly proficient at breaking into government and corporate computer networks, which helped change the everyday meaning of the word "hacker".

Today's hackers are people who gain unauthorized access to computers and computer networks.

Typically, you need a login name and password to access a computer system, but good hackers are adept at guessing short/predictable passwords. They employ brute-force methods to guess shorter passwords, and dictionary attacks to guess longer passwords.

Other techniques for obtaining login names and passwords are decidedly low-tech. Eavesdropping is common. **Dumpster diving**, looking through garbage for interesting bits of info, is used as well. **Social engineering**, the manipulation of a person inside the organization to gain access to confidential information, is used in large organizations where people don't know each other very well.

### Penalties for Hacking

Criminalized hacker-related activities by the Computer Fraud and Abuse Act:
- Transmitting code that causes damage to a computer system
- Accessing without authorization any computer connected to the Internet, even if no files are examined, changed, or copied
- Transmitting classified government info
- Trafficking in computer passwords
- Computer fraud
- Computer extortion

The max penalty is 20 years in prison and a $250,000 fine.

Another federal statute related to computer hacking is the ECPA, which makes it illegal to intercept telephone conversations, email, or any other data transmissions. It also makes it a crime to access stored email messages without authorization.

The use of the Internet to commit fraud/transmit funds can be prosecuted under the Wire Fraud Act and/or the National Stolen Property Act. Adopting the identity of another person to carry out an illegal activity is a violation of the Identity Theft and Assumption Deterrence Act.

### Selected Hacking Incidents

- info breach of foreign students at universities
- breaking into admissions software to see results
- Sesame Street porno replacement

### FBI and the Locked iPhone

- FBI wanted to open up mass shooter's work iPhone
- Apple and FBI fought

### Case Study - Firesheep

Only a small fraction of the info transported by the Interned is encrypted because encryption makes communications slower and more expensive. The widespread use of Wi-Fi has exposed a vulnerability caused by Internet packets being sent in the clear. A Wi-Fi network uses radio signals to communicate between devices. If the wireless access point isn't using encryption, it's easy for devices within range to snoop on the network traffic.

**Sidejacking** is the hijacking of an open Web session by the capturing of a user's cookie, giving the attacker the same privileges as the user on that Web site.

In 2010, Eric Butler released an extension to the Firefox browser called Firesheep, which made it easy for a Firefox user to sidejack open Web session. Butler relased it as free, open-source software to send a message about the lack of security that the organizations who are managing Web sites provide.

## 7-3 Malware

- malicious software

### Viruses

a piece of self-replicating code embedded within another program called the **host**. When a user executes a host program infected with a virus, the virus executes first. It then finds another executable store in the computer's file system and infects the executable. After doing this, the virus allows the host program to execute, which is what the user expected to happen.

Because a virus is attached to a host program, you may find viruses anywhere you can find program files. Today, many viruses are spread via email attachments.

Some viruses are fairly innocent; others are malicious and can cause significant damage to a person's file system.

Commercial antivirus software packages allow users to detect and destroy viruses lurking on their computers. To be most effective, users must keep the antivirus up-to-date by downloading patterns corresponding to the latest viruses.

### The Internet Worm

A **worm** is a self-contained program that spreads through a computer network by exploiting security holes in the computers connected to the network.

The first worm was made by Robert Tappan Morris Jr.

Morris entered the graduate program in CS at Cornell in the fall of 1988. He became intrigued with the idea of creating a computer worm that would exploit bugs he had found in three Unix applications: ftp, sendmail, and fingerd. 

The goal of the worm was to infect as many computers as possible. It wouldn't destroy or corrupt data files on the machines it infected.

On Nov 2, 1988, Morris learned that a fix for the ftp bug had been posted to the Internet. However, nobody had posted fixes to the other two bugs Morris knew about. 

After launching the worm, it quickly spread to thousands of computers. Unfortunately, due to several bugs in the worm's programming, computers became infected with hundreds of copies of the worm, causing them to crash every few minutes or become practically unresponsive.

### Sasser

The Sasser worm, launched in 2004, exploited a previously identified security weakness with PCs running the Windows OS. The effects of the worm were relatively benign; infected computers simply shut down shortly after booting. 

### Instant Messaging Worms

Choke and Hello, which appeared in 2001, were early worms that hit instant messaging systems.

### Conficker

appeared on Windows PCs in 2008, notable because of its persistence. The purpose was only to propagate.

### Cross-Site Scripting

another way in which malware may be downloaded w/o a user's knowledge. Web sites that allow users to read what other users have posted are vulnerable this; the attacker injects a client-side script into a Web site. When an innocent user visits the site sometime later, the user's browser executes the script, which may steal cookies, track user activity, or perform other malicious actions.

### Drive-By Downloads

In some cases, simply visiting a compromised Web site can result in the unintentional downloading of software, called a **drive-by download**.

### Trojan Horses and Backdoor Trojans

a malicious computer program designed to deceive users by concealing a sinister purpose behind a benign capability.

A backdoor Trojan is a Trojan horse that gives the attacker access to the victim's computer.

### Ransomware

Malware designed to extort money from the victim of the attack.

### Rootkits

A set of programs that provide privileged access to a computer. Once installed, a rootkit is activated every time the computer is booted.

### Spyware/Adware

spyware is a program that communicates over an Internet connection w/o the user's knowledge/consent. Spyware programs can monitor Web surfing, log keystrokes, take snapshots, and send reports back to a host computer. Spyware is often part of a rootkit. Adware is a type of spyware that displays pop-up ads related to what the user is doing.

### Bots and Botnets

A bot is a particular kind of backdoor Trojan that responds to commands sent by a command-and-control program located on an external computer. A collection of bot-infected computers is called a botnet, and a person who controls a botnet is called a bot herder.

### Security Risks Associated with BYOD

The "bring your own device" movement brings numerous benefits:
- reduced hardware/software expenditures
- more comfortable device usage, increasing productivity and job satisfaction
harms:
- company data may be compromised if the employee's device is stolen
- If the employee's device is insecure, it may provide an avenue for a malevolent agent to break into the company's network.

To address security concerns, companies establish BYOD policies:
- What are the security standards for personal devices (password requirements, antiviruses)
- What applications are employees allowed to run from their personal devices
- what is the level of support for personal devices that the company's IT department will provide
- Does the company have the right to erase all data on a personal device that has been stolen
- How will company data be removed from the devices of employees who are leaving the company

## 7-4 Cyber Crime and Cyber Attacks

### Phishing and Spear Phishing

a large-scale effort to gain sensitive info from gullible computer users. 

Spear phishing is a variant of phishing in which the attacker selects email addresses that target a particular group of recipients or even one particular person. 

### SQL Injection

a method of attacking a database-driven Web application that has improper security. The attacker accesses the application like any other client of the application, but by inserting (injecting) an SQL query into a text string from the client to the application, the attacker can trick the application into returning sensitive info.

### DoS and DDoS

A denial-of-service (DoS) attack is an intentional action designed to prevent legitimate users from making use of a computer service.

A distributed DoS attack (DDoS) consists of the attacker renting access to a botnet and having it attack a targeted system.

### IoT Devices Co-opted for DDoS Attack

IoT devices are relatively easy for malicious actors to co-opt because many people install them without changing their passwords from the factory default settings. Some inexpensive devices come with no password protections at all.

### Cyber Crime

#### Jeanson James Ancheta

created 400,000 bot strong botnet and rented it out.

#### Pharmamaster

Spammer that launched a massive DDoS attack targeting antispam software.

#### Albert Gonzalez

Used an SQL injection attack to steal more than 130 million credit and debit card numbers.

#### Avalanche Gang

Responsible for a majority of phishing attacks.

### Politically Motivated Cyber Attacks

A cyber attack is a "computer-to-computer attack that undermines the confidentiality, integrity, or availability of a computer or information resident on it".

#### Estonia

DDoS attack from Russia in 2007 on Estonia's internet

#### Georgia

More DDoS attacks from Russia in 2008.

Even more DDoS attacks in 2009

#### Exiled Tibetan Government

backdoor Trojans targeting the Dalai Lama and other Tibetans in a surveillance effort, 2008

#### US and South Korea

DDoS attack on governmental agencies and commercial Web sites in the US and South Korea, 2009.

#### Iran

Stuxnet worm in 2009 attacking SCADA (supervisory control and data acquisition) systems in Iran, cooperative effort between the US and Israel.

#### Cyber Espionage Attributed to the People's Liberation Army

#### Anonymous

A **hacktivist** is a "computer hacker whose activity is aimed at promoting a social or political cause". Anonymous is a loosely organized international movement of hacktivists, and the members are called Anons.

- Attack on the Church of Scientology
- Operation Payback against the RIAA, MPAA, Aiplex, and US Copyright Office, 2009
- Arab Spring, 2011
- 2012, pretty much continuing Operation Payback
- Holocaust Memorial Day in 2013, attack on Israeli Web sites
- 2014 attack on City of Cleveland website to protest killing
- 2015 condemnation of terrorist attack on the Paris office of satirical magazine *Charlie Hebdo*. 

## 7-5 Online Voting

### Motivation

Confusion on keypunch voting machine

### Proposals

Many states replaced paper-based systems with direct-recording electronic voting machines.

Others have suggested that voting via the Internet be used. 

### Ethical Evaluation

Benefits:
- Online voting would give people who ordinarily couldn't get to the polls the opportunity to cast a ballot from their homes
- votes cast via the Internet could be counted much more quickly than votes cast on paper
- Electronic votes would not have any of the ambiguity associated with physical votes
- Elections conducted online would cost less money than traditional elections
- Online voting would eliminate the risk of somebody tampering with a ballot box containing physical votes

Risks:
- Online voting is unfair because it gives an unfair advantage to those who are financially better off.
- The same system that authenticates the voter also records the ballot, which makes it difficult to preserve the privacy of the voter
- Online voting increases the opportunities for vote solicitation and vote selling
- A Web site hosting an election is an obvious target for a DDoS attack
- If voting is done from home computers, the security of the election depends on the security of those home computers:
	- A virus could change a person's vote w/o that person even suspecting what had happened
	- A backdoor Trojan could allow a person's vote to be observed by an outsider
	- An attacker could fool a user into thinking he/she was connected to the vote server when in actuality he/she was connected to a phony vote server

Any election system that relies upon the security of PCs managed by ordinary citizens will be vulnerable to electoral fraud.









---
# *References*
![[Ethics for the Information Age - Michael J. Quinn.pdf]]