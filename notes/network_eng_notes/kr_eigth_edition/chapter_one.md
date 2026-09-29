## 1.1 What is the Internet?

### Computer Networks and the Internet (the nuts & bolts description)

 - hosts / end systems - the consumer utilized - devices connected to a computer network (namely the Internet)

 - end systems are connected together by a network of communication links and packet switches

 - transmission rate - how we measure the rate at which data is transmitted by different communication links (measured in bits / second)

 - packets - small packages of information sent through a network from one end system to another

 - packet switch - takes a packet arriving on one of its incoming communication links and forwards that packet on one of its outgoing links (two most prominent kinds of packet switches: routers and link-layer switches)

 - The sequence of communication links and packet switches traversed by a packet from the sending end system to the receiving end system is known as a **route** or **path** through the network.

 - Think of a computer network with packet switches like a highway / road system. There are factories / buildings with cargo trying to send each other their product. So the product gets split into multiple **packets** or trucks, which then travel independently through the networks' roads / **communication links** and are trafficked accordingly at whatever intersections / **packet switches** they come across. The factory buildings themselves that do the sending and the receiving are the end systems.

 - End systems access the Internet through **Internet Service Providers (ISPs)**
 - examples of ISPs:
    - residential ISPs - local cable / telephone companies
    - corporate ISPs
    - university ISPs
    - ISPs that provide WiFi access in airports, hotels, coffee shops, and other public places
    - cellular data ISPs
 
 - Each ISP is in itself, a network of packet switches and communciation links, providing a variety of types of network access to the end systems
 - ISPs also provide Internet access to content providers, connecting servers directly to the Internet
 - The ISPs that provide access to end systems must also be interconnected (lower tier)
 - There are ISPs that consist of high-speed routers interconnected with high-speed fiber-optic links which connect the lower tier ISPs to each other (higher tier)
 - Each ISP is managed independently and runs the IP protocol and conforms to certain naming and address conventions

 - End systems, packet switches, and other pieces of the Internet run **protocols** that control the sending and receiving of information within the Internet

 - The **Transmission Control Protocol (TCP)** and the **Internet Protocol (IP)** are two of the most important protocols in the Internet
 - IP specifies the format of the packets sent and received among routers and end systems
 - **TCP/IP** refers to the Internet's principal protocols

 - **Internet Standards** are developed by the **Internet Engineering Task Force (IETF)**
 - the **IETF** standards documents are called **requests for comments (RFCs)** because RFCs started out as general requests for comments (hence the name) to resolve network and protocol design problems that faced the precursor to the Internet.
 - RFCs define protocols such as TCP, IP, HTTP (for the web), and SMTP (for e-mail). There are currently 9000 RFCs.
 - Other bodies also specify standards for network components, most notably for network links. (e.g. The **IEEE 802 LAN Standards Committee**
    specifies the Ethernet and wireless WiFi standards).


### Services Description of the Internet

 - The Internet can be described as: *an infrastructure that provides services to applications*

 - Internet applications include mobile smartphone and tablet applications, including Internet messaging, mapping with real-time road-traffic information, music streaming movie and television streaming, online social media, video conferencing, multi-person games, and location-based recommendation systems; those applications are said to be **distributed applications** since they involve multiple end systems that exchange data with each other.
 - ***NOTE***: Internet applications run on end systems, and NOT in the packet switches in the network core. Although packet switches facilitate the exchange of data among end systems, they are not concerned with the application that is the source or sink of data

 - End systems attached to the Internet provide a **socket interface** that specifies *how a program running on one end system asks the Internet infrastructure to deliver data to a specific destination program running on another end system*

 - The Internet provides services to applications in a similar way the postal service provides mail senders / receivers services

### What is a Protocol?

 - A **protocol** defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and or receipt of a message or other event



## 1.2 The Network Edge

 - The devices that sit at the edge of computer networks are called hosts / end systems (they mean the same thing here)
 - Somtimes, **hosts** are divided into two categories: **clients** and **servers**
 - Informally...
    - clients: desktops, laptops, smartphones, and so on~
    - servers: powerful machines that store and distribute Web pages, stream video, relay e-mail, and so on~
 - Most of the servers we receive information from today reside in large **data centers**


### Access Networks

 - **access network** - the network that physically connects an end system to the first router (also known as the "edge router") on a path from the end system to any other distant end system

### Home Access: DSL, Cable, FTTH, and 5G Fixed Wireless

 - The two most prevalent types of broadband (high speed and always on Internet) residential access networks are **digital subscriber line (DSL)** and **cable**

 - A residence typically obtains **DSL** Internet access from the same local telephone company (telco) that provides its wired local phone access; in
    this case, when a digital subscriber line is used, a home's telephone company is also it's internet service provider
 - In that particular case, a customer's DSL modem uses the existing telephone line exchange data with a **digital subscriber line access multiplexer (DSLAM)** located in the telco's local central office (CO). The home's DSL modem takes digital data and translates it to high-frequency tones for transmission over telephone wires to the CO; the analog signals from many such houses are translated back into digital format at the DSLAM.
 - on the customer's side, a splitter separates the data and telephone signals arriving to the home and forwards the data signal to the DSL modem.

 - While **DSL** makes use of the telco's existing local telephone infrastructure, **cable Internet access** makes use of the cable television company's existing cable television infrastructure.
 - The 'cable head' on the ISP's side is connected to residential / neighborhood-level junctions via fiber optic cables, which then connect to individual homes / apartments with coaxial cable. Since both cable types are used, this system is often referred to as hybrid fiber coax.
 - Cable internet access requires special modems called **'cable modems'**; like a DSL modem, cable modems are external devices that connect to the home PC that translates digitally formatted information to what would be sent in traditional cable, then a **cable modem termination system (CMTS)** translates the analog signal back into a digital format at the cable head end.
 - Cable modems divide the HFC network into two channels (upstream and downstream); access is typically asymmetric (different transmission rates for upstream and downstream channels)

 - **upstream channel** - the channel that carries traffic from the end system (host) toward the ISP
 - **downstream channel** - the channel that carries traffic from the ISP to toward the end system (host)
 - Cable Internet access is a shared broadcast medium -> affects download speeds depending on host activity; since the upstream channel is also shared, a distributed multiple access protocol is needed to coordinate transmissions and avoid collisions.

 - **fiber to the home (FTTH)** - an optical fiber path is provided to connect a CO directly to the home.
 - Several competing technologies for optical distribution from the CO to the homes. The simplest optical distribution network is called direct fiber, with one fiber leaving the CO for each home. But it's more common for each fiber leaving the central office to be shared by many homes with a splitter within close proximity of the homes sharing the fiber that splits into individual, customer-specific fibers.
 - There are 2 competing 
