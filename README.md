# Google Cybersecurity Professional Certificate - Analyze Network Attacks

## Table of Contents

- [Objectives](#objectives)
- [Scenario](#scenario)
- [Wireshark Log](#wireshark-log)
- [Incident Report](#incident-report)

## Objectives

The objective of this activity is to analyze a scenario involving a customer who experiences a security issue when accessing the company website and identify the cause of the service interruption.

## Scenario

You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like.

One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor.

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

## Wireshark Log

Logs with the color **red** are server interactions with the attacker's IP address, **yellow** are failed communications between a legitimate client and the web server, and **green** are successful communication between a legitimate client and the server.

| Color  | No. | Time      | Source        | Destination   | Protocol | Info                                            |
| ------ | --- | --------- | ------------- | ------------- | -------- | ----------------------------------------------- |
| red    | 52  | 3.390692  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 53  | 3.441926  | 192.0.2.1     | 203.0.113.0   | TCP      | 443->54770 [SYN, ACK] Seq=0 Win=5792 Len=120... |
| red    | 54  | 3.493160  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [ACK] Seq=1 Win=5792 Len=0...        |
| green  | 55  | 3.544394  | 198.51.100.14 | 192.0.2.1     | TCP      | 14785->443 [SYN] Seq=0 Win=5792 Len=120...      |
| green  | 56  | 3.599628  | 192.0.2.1     | 198.51.100.14 | TCP      | 443->14785 [SYN, ACK] Seq=0 Win=5792 Len=120... |
| red    | 57  | 3.664863  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| green  | 58  | 3.730097  | 198.51.100.14 | 192.0.2.1     | TCP      | 14785->443 [ACK] Seq=1 Win=5792 Len=120...      |
| red    | 59  | 3.795332  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=120...      |
| green  | 60  | 3.860567  | 198.51.100.14 | 192.0.2.1     | HTTP     | GET /sales.html HTTP/1.1                        |
| red    | 61  | 3.939499  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=120...      |
| green  | 62  | 4.018431  | 192.0.2.1     | 198.51.100.14 | HTTP     | HTTP/1.1 200 OK (text/html)                     |
| green  | 63  | 4.097363  | 198.51.100.5  | 192.0.2.1     | TCP      | 33638->443 [SYN] Seq=0 Win-5792 Len=120...      |
| red    | 64  | 4.176295  | 192.0.2.1     | 203.0.113.0   | TCP      | 443->54770 [SYN, ACK] Seq=0 Win-5792 Len=120... |
| green  | 65  | 4.255227  | 192.0.2.1     | 198.51.100.5  | TCP      | 443->33638 [SYN, ACK] Seq=0 Win-5792 Len=120... |
| red    | 66  | 4.256159  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| green  | 67  | 5.235091  | 198.51.100.5  | 192.0.2.1     | TCP      | 33638->443 [ACK] Seq=1 Win-5792 Len=120...      |
| red    | 68  | 5.236023  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| green  | 69  | 5.236955  | 198.51.100.16 | 192.0.2.1     | TCP      | 32641->443 [SYN] Seq=0 Win-5792 Len=120...      |
| red    | 70  | 5.237887  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| green  | 71  | 6.228728  | 198.51.100.5  | 192.0.2.1     | HTTP     | GET /sales.html HTTP/1.1                        |
| red    | 72  | 6.229638  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| yellow | 73  | 6.230548  | 192.0.2.1     | 198.51.100.16 | TCP      | 443->32641 [RST, ACK] Seq=0 Win-5792 Len=120... |
| red    | 74  | 6.330539  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| green  | 75  | 6.330885  | 198.51.100.7  | 192.0.2.1     | TCP      | 42584->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 76  | 6.331231  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| yellow | 77  | 7.330577  | 192.0.2.1     | 198.51.100.5  | TCP      | HTTP/1.1 504 Gateway Time-out (text/html)       |
| red    | 78  | 7.331323  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| green  | 79  | 7.340768  | 198.51.100.22 | 192.0.2.1     | TCP      | 6345->443 [SYN] Seq=0 Win=5792 Len=0...         |
| yellow | 80  | 7.340773  | 192.0.2.1     | 198.51.100.7  | TCP      | 443->42584 [RST, ACK] Seq=1 Win-5792 Len=120... |
| red    | 81  | 7.340778  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 82  | 7.340783  | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 83  | 7.439658  | 192.0.2.1     | 203.0.113.0   | TCP      | 443->54770 [RST, ACK] Seq=1 Win=5792 Len=0...   |
| red    | 119 | 19.198705 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 120 | 19.521718 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| yellow | 121 | 19.844731 | 192.0.2.1     | 198.51.100.9  | TCP      | 443->4631 [RST, ACK] Seq=1 Win=5792 Len=0...    |
| red    | 122 | 20.167744 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 123 | 20.490757 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 124 | 20.813770 | 192.0.2.1     | 203.0.113.0   | TCP      | 443->54770 [RST, ACK] Seq=1 Win=5792 Len=0...   |
| red    | 125 | 21.136783 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 126 | 21.459796 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 127 | 21.782809 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 128 | 22.105822 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 129 | 22.428835 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 130 | 22.751848 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 131 | 23.074861 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 132 | 23.397874 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 133 | 23.720887 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 134 | 24.043900 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 135 | 24.366913 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 136 | 24.689926 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 137 | 25.012939 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 138 | 25.335952 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 139 | 25.658965 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 140 | 25.981978 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 141 | 26.304991 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 142 | 26.628004 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 143 | 26.951017 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 144 | 27.274030 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 145 | 27.597043 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 146 | 27.920056 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 147 | 28.243069 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 148 | 28.566082 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 149 | 28.889095 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 150 | 29.212108 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 151 | 29.535121 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |
| red    | 152 | 29.858134 | 203.0.113.0   | 192.0.2.1     | TCP      | 54770->443 [SYN] Seq=0 Win=5792 Len=0...        |

## Incident Report

According to the given logs, a potential cause for the website's connection timeout error message is a DoS attack. The logs showed that the web server stopped responding after it was flooded with SYN packet requests making the attack possibly a SYN flood attack.

With the TCP protocol, a three-way handshake occurs between the client and the server. The handshake consists of a SYN packet being sent from the source to the destination, the destination replies with SYN-ACK packet to accept the connection request, and finally an ACK packet is sent from the source to the destination acknowledging the permission to connect.

In the case of a SYN flood attack, a malicious actor will send a large amount of SYN packets at once, overloading the server until it ran out of resources to make a legitimate TCP connections.

The logs indicate that the web server was ovewhelmed with the amount of SYN requests from the malicious actor therefore being unable to make connections to legitimate visitors that receives a connection timeout message instead.

## Learning Experience

This activity taught me about reading Wireshark logs and how to analyze those logs to determine if an attack is happening, and what kind of attack is being done.

This activity focuses on reading the log and determining why a connection between a legitimate client is not working and it can be seen that a DoS attack, specifically a SYN flood attack is happening due to the large amount of SYN packets being sent to the server.
