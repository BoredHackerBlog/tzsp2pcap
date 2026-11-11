# TITLE: tzsp2pcap

## Changes

When I was running this in one of my VMs, I got the following error:

```
socket(): Address family not supported by protocol
Could not setup tzsp listener
```

I looked through the code and it was doing ipv6 socket (diff here: https://github.com/BoredHackerBlog/tzsp2pcap/commit/c649418cac9a5bca90a10ea2e4c57a3079459c1f)

I had AI change it to use ipv4.

# AI Warning
Code was edited by AI and has not been tested for stability or other bugs!!

Model Provider: Nvidia Model: nemotron-3.5-super-vl-120b-a12b Agent: Hermes Agent

Why AI? I wanted to spend more time on my project instead of working on getting this code working. 

# Usage
Install gcc, make, libpcap-dev and run the make command to build the binary

# Introduction
This is a simple utility to listen for [[http://en.wikipedia.org/wiki/TZSP][TaZmen Sniffer Protocol]] (TZSP)
packets and output the contents on stdout in pcap format. It has only
been lightly tested with Mikrotik RouterOS products, and may need
alterations to work with other devices.

# Example usage
: tzsp2pcap -f | wireshark -k -i -
: tzsp2pcap -o "file.pcap" -C 1000000 # rotate file every 1MB (file.pcap.1, file.pcap.2, etc)
: tzsp2pcap -o "file_%s.pcap" -G 10 # create new file every 10 seconds (file_UNIXTIMESTAMP.pcap)
: tzsp2pcap -o "file.pcap" -C 1000000 -z gzip # rotate file every 1MB and gzip it (file.pcap.1.gz, file.pcap.2.gz, etc)
