<h1>Network Traffic Analysis with tcpdump</h1>

<h2>Description</h2>
Capture and analyze live network traffic using tcpdump. Use Linux commands in the Bash shell to complete these steps.
<br />
<br />
<h2>Task 1. Identify network interfaces</h2>

Used ifconfig to identify the interfaces that are available:

sudo ifconfig

![1](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/3fa04b9a-674e-4b2f-84b9-dfce18627747)

Used tcpdump -D to identify the interface options available for packet capture:

sudo tcpdump -D

![2](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/eaa1a632-37d1-464c-945c-f9ea58366c94)

<h2>Task 2:  Filter live network packet data from the eth0 interface with tcpdump</h2>

sudo tcpdump -i eth0 -v -c5

![3](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/c6152fdb-fec6-4d23-ad6a-bb6494ac8729)


This command ran tcpdump with the following options:
- i eth0: Capture data specifically from the eth0 interface.
- v: Display detailed packet data.
- c5: Capture 5 packets of data

Example of a packet:

![4](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/a09ae713-501f-4d6e-ab2d-1ce33f4d73c2)

Components:

the first field is the packet's timestamp, followed by the protocol type, IP:

![5](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/ae46c73c-ef59-4ee5-9376-9fa098116700)

The verbose option, -v, has provided more details about the IP packet:

![6](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/ef0b5650-93af-484a-ab45-90886939720d)

In the next section, the data shows the systems that are communicating with each other:

![7](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/ca1593be-1710-4cc2-bd93-8164faa5453e)

The remaining data filters the header data for the inner TCP packet:

![actually 8](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/21859cc6-05fc-4d8c-b17c-e6584da14773)

<h2>Task 3. Capture network traffic with tcpdump</h2>

Capture packet data into a file called capture.pcap:

sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &

![8](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/10b15671-01aa-4b1e-afc3-8f82428c346d)

This command ran tcpdump in the background with the following options:
- i eth0: Capture data from the eth0 interface.
- nn: Do not attempt to resolve IP addresses or ports to names.This is best practice from a security perspective, as the lookup data may not be valid. It also prevents malicious actors from being alerted to an investigation.
- c9: Capture 9 packets of data and then exit.
port 80: Filter only port 80 traffic. This is the default HTTP port.
- w capture.pcap: Save the captured data to the named file.
- &: This is an instruction to the Bash shell to run the command in the background.

Used curl to generate some HTTP (port 80) traffic:

curl opensource.google.com

![9](https://github.com/wilsonmantilla/tcpdump-traffic-analysis/assets/159208489/92d8e746-624f-4824-908e-58181fe03867)

When the curl command is used like this to open a website, it generates some HTTP (TCP port 80) traffic that can be captured.

Verified that packet data has been captured:

ls -l capture.pcap

















