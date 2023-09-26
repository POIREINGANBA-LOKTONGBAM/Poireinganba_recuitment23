# **!::CAR HACKING HANDBOOK::!**
---
---
---
### Why Car Hacking Is Good for All of Us?
1. It helps to understand how our car network works and how it communicates with its own system and outside world. This helps us troubleshoot problems.
2. Learning how our vehical's electronics work is very helpfull in overcomming the barrier where the monopolizes the in formation and data of the car electronic system.
3. Understanding communication system can help us better modify the parts and add aditional or third party components which increases the efficiency of the vehical.
4. We Discover undocumented or disabled features and utilizing them lets you use your vehicle to its fullest potential.
5. Learning how to hack our car will gives us the idea of weaknesses our car electronic system has and we can make it more secure.
6. Knowledge about car networking and communication systems can help the automotive industry in further advancing their tecnology and products.
---
---
## Chapter1: UNDERSTANDING THREAT MODELS~
### 1. Finding attack surfaces:
To find a vehical's attack surface, we need to understand its perimeter and doccument its environment. Also we need to consider all the ways data can get into a vehical.  
The key points to be considered are:
1. Type of signal recieved; Raio waves, key fobs(Radio), distance sensors.
2. Physical access, touch or motion.
3. If the vehical is electric, the way it charges.
For the interior:
1. The audio input.
2. The diagnostic ports.
3. Capibilities of the dashboard.
### 2. Threat Modelling:
To  threat model a car we need to collect information about the target and prepare a diagram to illustrate how the parts communicate with each other. We can threat model a car by drawing diagrams that show: level0- Attack surfaces, level1-Receiver(which recieves short range data), level2- internal workings of the car(Kernal).
### 3. Threat Identification:
Now that we have gone deeper into the internal workings of the car, we can figure out the various possible threats a car system has.  
Some of the high level threats are:
1. Remotely take over the vehical.
2. Shut down the vehical.
3. Spy on the vehical.
4. Unlock the vehical.
5. Steal a vehical.
6. Track a vehical.
7. Thwart safety systems.
8. Install malware on the vehical.

There are various levels how an attacker can enter the vehical's system: level1- Celular, wifi, keyfob, usb etc.(Eavesdrop, Jam signalls etc.), level2- Bluez, wpa_supplicant, Hsi, udev, Kavasa driver.(May be susceptible to exploitation, upload malicious malware etc)
### 3. Threat Rating system:
#### 1. The DREAD Rating System:
1. **Damage potential** How great is the damage?
2. **Reproducibility** How easy is it to reproduce?
3. **Exploitability** How easy is it to attack?
4. **Affected users** How many users are affected?
5. **Discoverabilty** How easy is it to find the vulnerability?

The following table gives an idea about the DREAD rataing catagory:

|   | Rating category | High  (3) | Medium (2) | Low (1) |
| - | --------------- | --------- | ---------- | ------- |
|D |Damage potential| Could subvert the security system and gain full trust, ultimately taking over the environment|Could leak sensitive information| Could leak trivial information|
|R |Reproducibility| Is always reproducible| Can be reproduced only during a specific condition or window of time| Is very difficult to reproduce, even given specific information about the vulnerability|
|E |Exploitability| Allows a novice attacker to execute the exploit| Allows a skilled attacker to create an attack that could be used repeatedly| Allows only a skilled attacker with in-depth knowledge to perform the attack|
|A |Affected users| Affects all users, including the default setup user and key customers| Affects some users or specific setups| Affects a very small percentage of users; typically affects an obscure feature|
|D |Discoverability| Can be easily found in a published explanation of the attack| Affects a seldom-used part, meaning an attacker would need to be very creative to discover a malicious use for it |Is obscure, meaning it’s unlikely attackers would find a way to exploit it|  

#### 2. CVSS: An Alternative to DREAD:
Itoffers many more categories and details than DREAD in three groups: 
base, temporal, and environmental. Each group is subdivided into sub 
areas—six for base, three for temporal, and five for environmental—for a 
total of 14 scoring areas.
### 4. Working with Threat Model Results:
Once we know the various threats in our system then we should go through the risk chart and modify or strengthen the weak spots. We can start creating countermeasures of the attack points to reduce the risk of a successful attack.
---
---
## Chapter2: BUS PROTOCOLS~
### The CAN Bus:
CAN runs on two wires: CAN high (CANH) and CAN low (CANL). CAN uses differential signaling i.e. It raises the voltage on one line and drops on the other in equal ammount.  
Differential signaling is used in environments that must be fault tolerant to noise, such as in automotive systems 
and manufacturing.  
**Fault tolerance** is a process that enables an operating system to respond to a failure in hardware or software. It makes sure that the Operating system runs even after the event of a fault.  
The two twisted-pair wires make up the bus and require the bus to be terminated on each end. A 120-ohm resistor is attached across both wires on the termination ends.
### The OBD-II Connector:
The OBD II connector also known as diagnostic link connector communicates with the vehicals internal networks. Can be found under the steering column or in hidden elseware in the dash in a relatively accessible place. some vehicles, you’ll find these connectors behind small access panels. They’ll typically be either black or white
### Finding CAN connections:
CAN wire's resting voltage is 2.5V. It fluctuates 1V {3.5 to 1.5}.  
The CANH and CANL connections on pins 6 and 14 of the OBD-II connector.
### CAN Bus Packet Layout:
1. **Standard Packet**:
   > 1. Arbitration ID: It is a broadcast message that identifies the id of the device trying to communicate.
   > 2. Identifier extension (IDE): This bit is always zero for standard CAN.
   > 3. Data length code(DLC): It gives the size of the data which ranges from  0 to 8 bytes.
   > 4. Data: It is the data itself. Maximum size is 8 bytes.
2. **Extended Packets**:
   > They are like the Standard ones but can be chained togther to make longer ids. Extended packets are designed to fit inside standard CAN formatting in order to maintain backward compatibility. So if a sensor doesn’t have support for extended packets, it won’t break if another packet transmits extended CAN packets on the same network.
3. **The ISO-TP Protocol**:
   > The most common use of ISO-TP is for diagnostics (see “Unified Diagnostic Services” on page 54) and KWP messages (an alternative protocol to CAN), but it can also be used any time large amounts of data need to be transferred over CAN.
4. **The CANopen Protocol**:
   > CANopen breaks down the 11-bit identifier to a 4-bit function code and 7-bit node ID—a combination known as a communication object identifier (COB-ID). A broadcast message on this system has 0x for both the function code and the node ID. CANopen is seen more in industrial settings than it is in automotive ones.
5. **The GMLAN Bus**:
   > Implementation by General Motors. The GMLAN bus consists of a single-wire low-speed and a dualwire high-speed bus. It is used to transport noncritical information for things like the infotainment center, HVAC controls, door locks, immobilizers etc.
### The SAE J1580 Protocol:
There are two types of J1850 protocols: pulse width modulation (PWM) and variable pulse width (VPW). These bus systems are older and slower than CAN but cheaper to implement. It is an intermodule data communication network for the sharing of parametric information passed in frames (messages) between all vehicle electronic modules connected to the Class B bus
### The PWM Protocol:
PWM uses differential signaling on pins 2 and 10 and is mainly used by Ford. It operates with a high voltage of 5V and at 41.6Kbps, and it uses dual-wire differential signaling, like CAN. PMW has a fixed-bit signal, so a 1 is always a high signal and a 0 is always a low signal. Other than that, the communication protocol is identical to that of VPW. The differences are the speed, voltage, and number of wires used to make up the bus.
### The VPW Protocol:
VPW, a single-wire bus system, uses only pin 2 and is typically used by General Motors and Chrysler. VPW has a high voltage of 7V and a speed of 10.4Kbps. It uses time-dependent signaling
### The Keyword Protocol and ISO 9141-2:
The Keyword Protocol 2000 (ISO 14230), also known as KWP2000, uses 
pin 7 and is common in US vehicles made after 2003. Messages sent using 
KWP2000 may contain up to 255 bytes.
### Summary:
When working on our target vehicle, we may run into a number of different buses and protocols. When we do so, examine the pins that our OBD-II connector uses for our particular vehicle to help us determine what tools we’ll need and what to expect when reversing our vehicle’s network. Not all bus lines are exposed via the OBD-II connector, and when looking for a certain packet, it may be easier to locate the module and bus lines leaving a specific module in order to reverse a particular packet.
