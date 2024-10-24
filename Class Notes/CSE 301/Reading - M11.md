202406140316
Meta Tags: #class
Tags: [[ethics]]

# Reading - M11

>Chapter 8

## 8-1 Introduction

>When computerized systems work correctly, they save us time and money and enable us to accomplish a great deal in a day. When they fail, the benefits can turn into harms. Failures of computer-driven systems can result in lost time, lost money, and in extreme cases, injury or even death.

## 8-2 Data-Entry or Data-Retrieval Errors

### Disenfranchised Voters

November 2000 general election, Florida disqualified thousands of voters because preelection screening identified them as felons. However, they actually just had misdemeanors. 

### False Arrests

Stories of police making false arrests based on NCIC info:
- Sheila Jackson Stossier, confused with Shirley Jackson.
- Roberto Hernandez, mistaken twice
- Terry Dean Rogan's driver's license was used by another person to commit crimes, the real Terry was arrested 5 times over a period of 14 months.

## 8-3 Software and Billing Errors

### Errors Leading to System Malfunctions

- Bug in Qwest's billing software caused very high charges
- US Department of Agriculture's understatement of prices, costing beef producers between $15-20 million
- 1996 UPS software error resulted in 2 weeks' worth of mail being returned to the senders
- University of Pittsburgh study revealed that computer spelling/grammar checkers actually increased errors
- September 2008 and May 2009, NYC families charged too much rent.
- 2010, 450 prison inmates w/ high risk of violence were mistakenly released.

### Errors Leading to System Failures

- fully computerized ambulance dispatch system caused as many as 20 people to die in London.
- March 1, 2003, Japan's air traffic control system went down for an hour at the same time as the backup system.
- New lab computer system at LA County+USC Medical Center became backlogged the day after it was turned on.
- August 2005, Malaysia Airlines Flight software error on the Boeing 777 caused it to go out of control for a period of time.
- 2013, 2015, NASDAQ shut down for hours of time because of computer-related issue
- Black Hat conference in Las Vegas in 2011, Jay Radcliffe demonstrated insulin pump hack.
- July 2015, 2 researchers demonstrated how they could hack wirelessly into a Jeep Cherokee.

## 8-4 Notable Software System Failures

**embedded system** - a computer used as a component of a larger system.

Software controllers are faster, more sophisticated, accept more input data, cost less, use less energy, and don't wear out. However, they are not reliable.

Most embedded systems are **real-time systems**, computers that process data from sensors as events occur. These **must** meet deadlines.

### Patriot Missile

- Originally designed by the US Army to shoot down airplanes, used in the 1991 Gulf War
- Was not very effective at all, despite seeming so superficially
- Failed because of a software error - *truncation*, because values were stored in a floating-point variable with insufficient precision. The truncation errors accumulated over 100 hours, resulting in the tracking system being off by a fraction of a second. This was enough to prevent the missile battery from locating the other missile.

### Ariane 5

- satellite launch vehicle designed by the French space agency and European Space Agency
- a software error caused the nozzles on the solid boosters and the main rocket engine to swivel to extreme positions. As a result, the rocket veered sharply off course. 
- the error was a piece of code that converted a 64-bit floating-point value into a 16-bit signed integer. Because of an overflow, an exception was raised; unfortunately, there was no exception-handling mechanism for this particular exception, so the onboard computers crashed.
- the piece of code had been part of the software for the Ariane 4. The engineers assumed based on the Ariane 4 that the 16-bit signed integer could store the horizontal velocity of the Ariane 5.

### AT&T Long-Distance Network

- January 15, 1990, AT&T's long-distance network suffered a significant disruption of service.
- The crash was brought about by a single line of code in an error-recovery procedure. All the switches entered a cycle of rebooting and sending out a signal that caused others to reboot if they were too busy. Because one switch rebooting would cause more traffic to go on another switch, this cycle just got worse and worse.

### Robot Missions to Mars

- NASA designed the $125 million Mars Climate Orbiter to facilitate communications between Earth and automated probes on the surface of Mars
- the spacecraft was lost because of a miscommunication between two support teams on Earth. One team used metric units, and the other used English units.
- The Mars Polar Lander also had its software fail as well.

### Denver International Airport

- Denver wanted to make a new airport, and signed a $193 million contract with BAE Automated Systems to design and build the automated baggage-handling system.
- The complexity of the system exceeded the ability of the development team to understand it.
	- Luggage carts were misrouted and failed to arrive at their destinations.
	- Computers lost track of where the carts were.
	- Bar-code printers didn’t print tags clearly enough to be read by scanners.
	- Luggage had to be correctly positioned on conveyors in order to load properly.
	- Bumpers on the carts interfered with the electric photocells.
	- Workers painted over electric eyes or knocked photo sensors out of alignment.
	- Light luggage was thrown off rapidly moving carts.
	- Luggage was shredded by automated baggage handlers.
	- The design did not consider the problem of fairly balancing the number of available carts among all the locations needing them.

### Tokyo Stock Exchange

- December 8, 2005, Mizuho Securities employee made a mistake that caused a large loss for the company, as a result of a bug in the Tokyo Stock Exchange trading program. 

### Direct-Recording Electronic Voting Machines

- Nearly 2 million ballots were not counted in the 200 US election because they register either no choice or multiple choices. 
- Many states chose to replace their previous voting methods with electronic DRE voting machines.
- Some voting irregularities were linked to DRE voting machines since 2002:
	- November 2002, programming error caused a touch-screen voting machine to fail to record 436 ballots cast in Wake County, North Carolina
	- 2003 Election in Boone County Indiana has a programming error that forced ballots to be recounted.
	- Florida's special election in January 2004, some voting machines reported that 134 voters hadn't voted for candidate, even though that wasn't an option. 
	- November 2004, initial printouts from all the DRE voting machines in LaPorte County, Indiana, reported less votes than it should have
	- In November 2004, a bug in the vote-counting software in DRE voting machines in Guilford County, North Carolina, caused the systems to begin counting backward after they reached a maximum count of 32,767.
	- In 2006, some Florida voters had a hard time voting for Democratic candidates; also, another election had more than 18000 votes not recorded.

The DRE systems had a lot of security weaknesses. As such, a lot of Americans were back to casting old-fashioned paper ballots by 2014.

## 8-5 Therac-25

- Linear accelerators create high-energy electron beams to treat shallow tumors and X-ray beams to reach deeper tumors.
- The Therac-25 was notoriously unreliable, giving massive overdoes to six patients in a 20-month period between June 1985 to January 1987. 

### Genesis

Atomic Energy of Canada Limited (AECL) and the French corporation CGR cooperated in the 70s to build two linear accelerators: the Therac-6 and the Therac-20. 

The distinguishing feature of the Therac series was the use of a DEC PDP 11 minicomputer as a "front end". The 6 and the 20 were capable of working independently of the PDP 11, and all of their safety features were built into the hardware.

After the Therac-20, AECL and CGR went their separate ways. AECL then made the Therac-25; unlike the 6 and the 20, the PDP 11 was an integral part of the device, which enabled AECL to reduce costs by replacing some of the hardware safety feature of the Therac-20 w/ software safety features in the Therac-25.

### Chronology of Accidents and AECL Responses

#### Marietta, Georgia, June 1985

was burned and suffered crippling injuries as a result of the overdose, and she sued AECL and the hospital in October 1985.

#### Hamilton, Ontario, July 1985

Machine turned on even though it displayed that it wasn't on, giving the patient a radiation overdose between 65 and 85 times the normal dose. Died of cancer in November 1985.

#### First AECL Investigation, July-September 1985

AECL introduced hardware and software changes to fix a microswitch problem, but the overdose problem wasn't discovered by the engineer.

#### Yakima, Washington, December 1985

Radiation overdose left the patient scarred and with a mild disability.

#### Tyler, Texas, March 1986

Dose monitor indicates way too little radiation, patient suffered acute pain and steadily lost bodily function until he died of the overdose 5 months later.

#### Second AECL Investigation, March 1986

Found no problems.

#### Tyler, Texas, April 1986

Same thing, but he died 3 week later instead of 5 months.

#### Yakima, Washington, January 1987

Some pattern of burns as the last incident, the patient died 3 months later.

#### Therac-25 Declared Defective, February 1987

FDA declared it to be defective; five month slater, after five revisions, AECL produced a corrective action plan that met the approval of the FDA.

### Software Errors

In the course of investigating the accidents, AECL discovered a variety of hardware and software problems. Two of the software errors are examples of **race conditions** (where 2 or more concurrent tasks share a variable, and the order in which they read or write the value of the variable can affect the behavior of the program).

### Postmortem

Some mistakes made by AECL in the design, development, and support of the system:
- AECL focused on identifying and fixing particular software bugs, which was too narrow of a approach
- The 25 has a lack of software/hardware devices to detect and report overdoses and shut down the accelerator immediately

Some lessons to be learned:
- race conditions are very hard to find
- software design needs to be as simple as possible
- design decisions must be documented to aid in the maintenance of the system
- the code must be reasonably documented at the time it is written
- reusing code doesn't always increase the quality of the final product

## 8-6 Tesla Version 7.0

### Introduction

In 2015, Tesla release a software update (7.0) that made Tesla the first automaker to release a product exhibiting Level 3 automation as defined by SAE International.

### May 2016 Fatal Accident

Tesla fanatic Joshua Brown was killed when his car crashed into the semitrailer portion of a semitrailer truck on a Florida highway.

Mobileye provided an explanation that the system was designed to avoid rear-end collisions, not to avoid vehicles crossing laterally. Tesla motors quickly release a clarification in which it noted that automatic braking didn't engage because the trailer was white, making it difficult to see, and it was tall, making its radar signature similar to that of an overhead sign.

### The Hand-off Problem

How can the computer ensure the driver is paying enough attention that it can pass over control in case of an emergency?

## 8-7 Uber Test-Vehicle Accident

### Introduction

Uber, in an effort to catch up with other companies like Tesla and Waymo, opened the Uber Advanced Technologies Center in January 2015.

### Shift to One Human Safety Operator

When Uber began testing the vehicles, it put 2 safety operators in the car. In the fall of 2017, Uber decided to remove the second safety operator. 

### Effort to Eliminate "Bad Experiences"

The reliability of Uber's system in March 2018 was far lower than that of more mature systems. 

Another problematic issue was that every two miles on average, its self-driving vehicles would startle passengers with a "bad experience", such as braking too quickly. 

Incorrectly identifying a danger when there is none is called a **false positive**, which is bad news; not only is it disconcerting to the passengers, it is dangerous. 

Engineers can modify a system to eliminate nearly all false positives, but that action risks making the system prone to **false negatives**, failing to identify a danger, and that problem is even worse.

### March 18, 2018, Accident

Because the vehicle required human intervention for emergency braking, an accident happened as a result of a safety operator not being attentive of the surroundings and a pedestrian jaywalking.

## 8-8 Computer Simulations

Errors in computer simulations can result in poorly designed products, mediocre science, and bad policy decisions.

### Uses

It plays a key role in contemporary science and engineering, as there are many reasons why a scientist/engineer may not be able to perform a physical experiment.

Computer simulations:
- model past events, such as when astrophysicists derive theories about the evolution of the universe
- understand the world around us; one of the first important uses of computer simulations was to aid in the exploration for oil
- predict the future, such as modern weather predictions

Of course, computer simulations can be wrong. This can be a result of not considering all inputs. 

### Validating Simulations

A computer simulation may produce erroneous results for 2 different reasons:
- the program may have a bug in it
- the model upon which the program is based may be flawed
**Verification** is the process of determining if the computer program correctly implements the model. **Validation** is the process of determining if the model is an accurate representation of the real system.

One way to validate a model is to make sure it duplicates the performance of the actual system; for example, automobile and truck manufacturers create computer models of their products and then test the products themselves.

Validating a model that predicts the future can introduce new difficulties. If we are predicting tomorrow's weather, it is reasonable to validate the model by waiting until tomorrow and seeing how well the prediction held up. However, if the model estimates a time way later, then you cannot validate it. However, you can validate the model by using it to *predict the present*.

A final way to validate a model is to see if it has credibility with experts and decision makers. 

## 8-9 Software Engineering

An engineering discipline focused on the production of software, as well as the development of tools, methodologies, and theories supporting software production.

1. Specification: defining the function to be performed by the software
2. Development: producing the software that meets the specifications
3. Validation: testing the software
4. Evolution: Modifying the software to meet the changing needs of the customer

### Specification

- focuses on determining the requirements of the system and the constraints under which it must operate
- results in a high-level statement of requirements and perhaps a mock-up of the UI that the users can approve. Software engineers also produce a low-level requirements statement that provides the details needed by those who are going to actually implement the software system.

### Development

- The first design is based on a high-level, abstract view of the system. The process of developing reveals ambiguities, omissions, or outright errors in the specification.
- gradually, the software engineers add levels of detail to the design

In a traditional design, the software system is viewed as a group of functions manipulating a set of shared data structures. In an **object-oriented design**, the software system is seen as a group of objects passing messages to each other.

Benefits:
1. Because each object is associated with a particular component of the system, the designs are easier to understand
2. Because each object hides its state and private data from other objects, other objects cannot accidentally modify its data items
3. Because objects are independent of each other, it is much easier to reuse components of a object-oriented system

### Validation

- ensuring the software satisfies the specification and meets the needs of the user
- Testing software is much harder than testing other engineered artifacts, since there are virtually infinite inputs and you can't really extrapolate small test results to big situations.

### Evolution

Successful software systems evolve over time to meet the changing needs of their users.

### Improvement in Software Quality

### Gender Bias

Unconscious gender bias can affect important design decisions.

### Bias in Training Data Sets for AI Systems

Bias can also be reflected onto AI systems.

## 8-10 Software Warranties and Vendor Liability

If perfect software is impossible, what should the rights of consumers be to get compensation when programs malfunction?

### Shrink-Wrap Warranties

Traditional consumer software was often called **shrink-wrap software** because of the plastic wrap surrounding the box containing the software and manuals.

Before, consumer software manufacturers provided no warranty for their products, but today many do.

### Are Software Warranties Enforceable❔

An early court case, *Step-Saver Data Systems v. Wyse Technology and The Software Link*, seemed to affirm the notion that software manufacturers could be held responsible for defective programs, despite what they put in their warranties. However, 2 later cases seemed to indicate the opposite. In *ProCD v. Zeidenberg*, the court ruled that the customer could be bound to the license agreement, even if it doesn't appear on the outside of the shrink-wrap box. *Mortenson v. Timberline Software* showed that a warranty disclaiming the manufacturer's liability could hold up in court.

### Should Software Be Considered a Product❔

When software is judged to be a good, the provisions of the Uniform Commercial code regarding damages and warranty can apply.  If software were to be considered a product, then the theory of strict liability would apply to the software manufacturer.

To date, courts in the US have resisted doing so because a software-controlled device may cause harm through no fault of the programmer.

## Summary

Computer are part of larger systems, and ultimately it is the reliability of the entire system that is important.

While it may be infeasible to provide redundant software systems, safety-critical systems should never rely completely upon a single piece of software.

---
# *References*
![[Ethics for the Information Age - Michael J. Quinn.pdf]]