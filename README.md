# Automation of a rainwater collection and treatment system
The code in this repository aims at automating the small homemade setup I created for water collection, treatment and distribution of rainwater as (hopefully) drinkable water.

## 1. Project limitations and warnings
This is a pet project by a DIY enthusiast for DIY enthusiasts, with a specific goal in mind. Its use comes with **no warranty whatsoever**. Please read the following disclaimers carefully and keep them in mind when using this repository's code or trying to replicate the setup I used:

### - Code reliability
As any code, and especially homemade by one person, it can (and will) crash. As I said, this is a pet project. I tried my best to make it robust and reliable; but still, things might break.

### - Water quality
Similarly, **the water quality is not guaranteed**! None of the sensors used here can prove water to be drinkable. At best, their readings and their evolution provide an insightful view of organic development proxies. The only way I know to properly guarantee water is drinkable remains to have it frequently tested.

### - Project life cycle
The code in this repository will probably not be expanded or maintained for long. If it works for me, I'll gladly shelve it for some time, until it might really need dependencies updates or even some light refreshing.

Therefore, I will probably not address the issues raised on the repository. You are still welcome to signal them on the dedicated tab if you wish.

### - Making it your own
If you plan on using this as a resource for your own project, you're welcome to fork it and adapt anything as you see fit. A shout-out will still be appreciated.

See `LICENSE` for further information about the MIT license this repository falls under.

## 2. Project overview

### 2.1. Main design constraints
As we personally depend on this code for our house's main water source, I aimed at making it as reliable, robust and dependable as possible.

It was also made with adaptability and a low power budget in mind.

**TODO**: Highest-level overview of the system

### 2.2. Logic hardware
I used 2 Raspberry Pi 4 microcomputers, along with several Raspberry Pi Pico 2 microcontrollers.

Having 2 microcomputers enables to split the operations between the 2 physically-separated facilities I had at home: one for collection and storage, and the other for treatment and distribution. Most of the automation work happens within the treatment facility, though. They still share the same base, for the sake of flexibility.

All of the hardware is represented using dedicated classes with a relatively precise classification. Don't hesitate to use that to your advantage to adapt the code for your needs.

### 2.3. Controlled elements

#### 2.3.1. Sensors
Many sensors will be included, mainly for water quality and flow monitoring

**TODO**

#### 2.3.2. Actuators
Quite a lot of actuators will be included, mainly valves and a few pumps (and even motors)

**TODO**

#### 2.3.3. Other elements the systems handles
**TODO**: power supply

### 2.4. Main technical features

#### 2.4.1. Language
The code is almost entirely in the latest stable minor core Python version that was compatible with the libraries used at the time of their inclusion.

SQLite is also used for logs, as well as for outboxes and inboxes in each microcomputer (*cf.* mention of transactional pattern for inter-facilities communication below).

#### 2.4.2. Intra-facilities communication
Within each facility, the microcomputer communicates with the mnicrocontrollers using Modbus and RS-485.

They are widely-used, free, industrial-grade standards for such applications.

RS-485 in particular helps a ton in the context of long cable distances, which proves necessary given for instance the length of some storage tanks or the distance between the treatment facility's microcomputer and the pump that delivers water from storage to treatment.

In the context of the Modbus protocol, the microcomputer acts as the conductor (*master*) and the microcontrollers as the operatives (*slaves*).

#### 2.4.3. Inter-facilities communication
In my use case, both facilities (meaning their respective microcomputers) only communicate with another, central microcomputer hosting an Internet-of-Things gateway, in a star architecture. Yet, the same protocols can be applied to (and are probably among the most relevant for) direct inter-facilities communication as well. Such a web-like architecture should not add too much complexity.

The protocols used are MQTT on Ethernet.

To ensure reliable communication between microcomputers even after a period of disconnection, the project also uses the transactional outbox and inbox patterns (with simple polling).

#### 2.4.4. Detailed schematics
**TODO**s:
- Relatively high-level overview of whole automation system
- Zoom in on the storage facility's automation
- Zoom in on the treatment facility's automation
- Zoom in on the treatment facility's power supply's management
