---
title: "Sample Headers"
description: Bytes in each capture format that are not packets
date: 2019-08-01
author: Ross Jacobs

summary: ''
weight: 90
draft: false
---

Using the available file headers on your system from [Capture Formats](/formats/format_usage/#determining-file-headers), we can determine what hex each capture type has in its header.
We do this by filtering out all packets and sending to xxd. If a capture type also has a footer, that too will be included here.

## Sample Capture Hex

```bash
bash$ formats=(5views commview erf k12text lanalyzer modpcap netmon1 netmon2 \
        nettl ngsniffer ngwsniffer_1_1 ngwsniffer_2_0 niobserver nokiapcap nsecpcap \
        pcap pcapng rh6_1pcap snoop suse6_3pcap visual)
bash$ tshark -w temp.pcap -c 1 # Capture only one packet for minimum capture
bash$ for i in ${formats[@]}; \
        do echo -e "\n# $i File Header"; \
        # Remove all packets by filtering by unused ipx
        tshark -r temp.pcap -Y ipx -F "$i" -w temp.file; \
        # Lanalyzer output is almost 188 lines long!
        orig="$(xxd -u temp.file)"; \
        trunc="$(xxd -u temp.file | head -n19)"; \
        echo -e "$trunc"
        if [[ $orig != $trunc ]]; then
          echo '# OUTPUT TRUNCATED'
        fi
      done

# 5views File Header
00000000: AAAA AAAA 2000 0000 0000 0100 1800 0000  .... ...........
00000010: 0010 0018 0000 0000 0000 0000 0000 0000  ................
00000020: 0700 0080 0400 0100 FCC7 445D 0000 0020  ..........D]...
00000030: 0400 0100 0000 0000                      ........

# commview File Header


# erf File Header
00000000: 0000 0000 0000 0000 9B04 0130 0000 0114  ...........0....
00000010: 1100 0000 0000 0000 0002 0008 0000 0000  ................
00000020: 0000 0000 FF00 0004 0000 0040 0010 0032  ...........@...2
00000030: 4475 6D70 6361 7020 2857 6972 6573 6861  Dumpcap (Wiresha
00000040: 726B 2920 332E 302E 3320 2876 332E 302E  rk) 3.0.3 (v3.0.
00000050: 332D 302D 6736 3133 3062 3932 6230 6563  3-0-g6130b92b0ec
00000060: 3629 0000 FF01 0004 0000 0078 0031 0037  6).........x.1.7
00000070: 496E 7465 6C28 5229 2043 6F72 6528 544D  Intel(R) Core(TM
00000080: 2920 6937 2D34 3737 3048 5120 4350 5520  ) i7-4770HQ CPU
00000090: 4020 322E 3230 4748 7A20 2877 6974 6820  @ 2.20GHz (with
000000a0: 5353 4534 2E32 2900 0011 002E 4D61 6320  SSE4.2).....Mac
000000b0: 4F53 2058 2031 302E 3134 2E35 2C20 6275  OS X 10.14.5, bu
000000c0: 696C 6420 3138 4631 3332 2028 4461 7277  ild 18F132 (Darw
000000d0: 696E 2031 382E 362E 3029 0000 FF03 0004  in 18.6.0)......
000000e0: 0001 0050 000C 0003 656E 3000 000D 0005  ...P....en0.....
000000f0: 5769 2D46 6900 0000 0011 002E 4D61 6320  Wi-Fi.......Mac
00000100: 4F53 2058 2031 302E 3134 2E35 2C20 6275  OS X 10.14.5, bu
00000110: 696C 6420 3138 4631 3332 2028 4461 7277  ild 18F132 (Darw
00000120: 696E 2031 382E 362E 3029 0000 0000 0000  in 18.6.0)......

# k12text File Header


# lanalyzer File Header
00000000: 0110 4C00 0105 5472 6163 6520 4469 7370  ..L...Trace Disp
00000010: 6C61 7920 5472 6163 6520 4669 6C65 0000  lay Trace File..
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000040: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000050: 0610 8000 4368 616E 6E65 6C31 0043 6861  ....Channel1.Cha
00000060: 6E6E 656C 3200 4368 616E 6E65 6C33 0043  nnel2.Channel3.C
00000070: 6861 6E6E 656C 3400 4368 616E 6E65 6C35  hannel4.Channel5
00000080: 0043 6861 6E6E 656C 3600 4368 616E 6E65  .Channel6.Channe
00000090: 6C37 0043 6861 6E6E 656C 3800 0000 0000  l7.Channel8.....
000000a0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000b0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000c0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000d0: 0000 0000 0B10 3600 5472 616E 7331 0000  ......6.Trans1..
000000e0: 0054 7261 6E73 3200 0000 5472 616E 7333  .Trans2...Trans3
000000f0: 0000 0054 7261 6E73 3400 0000 5472 616E  ...Trans4...Tran
00000100: 7335 0000 0054 7261 6E73 3600 0000 3510  s5...Trans6...5.
00000110: 9000 0000 0000 0000 0000 0000 0000 0000  ................
00000120: 0000 0000 0000 0000 0000 0000 0000 0000  ................
# OUTPUT TRUNCATED

# modpcap File Header
00000000: 34CD B2A1 0200 0400 0000 0000 0000 0000  4...............
00000010: 0000 0400 0100 0000                      ........

# netmon1 File Header
00000000: 5254 5353 0101 0100 B107 0C00 0300 1F00  RTSS............
00000010: 1000 0000 0000 0000 8000 0000 0000 0000  ................
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................

# netmon2 File Header
00000000: 474D 4255 0002 0100 B1D5 0600 0500 1000  GMBU............
00000010: 1100 0500 0400 0000 8000 0000 0000 0000  ................
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................

# nettl File Header
00000000: 5452 0064 0000 0000 0000 0080 2F74 6D70  TR.d......../tmp
00000010: 2F77 6972 6573 6861 726B 2E54 5243 3030  /wireshark.TRC00
00000020: 3000 0000 0000 0000 0000 0000 0000 0000  0...............
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000040: 0000 0000 5554 4300 0000 0000 0000 0000  ....UTC.........
00000050: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000060: 0042 2E31 312E 3131 0000 5500 0000 0000  .B.11.11..U.....
00000070: 0000 0039 3030 302F 3830 3000 0000 0406  ...9000/800.....

# ngsniffer File Header
00000000: 5452 534E 4946 4620 6461 7461 2020 2020  TRSNIFF data
00000010: 1A01 0012 0000 0003 0000 0000 00         .............

# ngwsniffer_1_1 File Header
00000000: 5843 5000 3030 312E 3130 3000 0000 0000  XCP.001.100.....
00000010: 0000 0000 0000 0000 8000 0000 8000 0000  ................
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000040: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000050: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000060: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000070: 0000 0000 0000 0000 0000 0000 0000 0000  ................

# ngwsniffer_2_0 File Header
00000000: 5843 5000 3030 322E 3030 3100 0000 0000  XCP.002.001.....
00000010: 0000 0000 0000 0000 8000 0000 8000 0000  ................
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000040: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000050: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000060: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000070: 0000 0000 0000 0000 0000 0000 0000 0000  ................

# niobserver File Header
00000000: 4F62 7365 7276 6572 506B 7442 7566 6665  ObserverPktBuffe
00000010: 7256 6572 7369 6F6E 3D31 352E 3030 0000  rVersion=15.00..
00000020: 6F00 0002 0200 4300 5468 6973 2063 6170  o.....C.This cap
00000030: 7475 7265 2077 6173 2073 6176 6564 2066  ture was saved f
00000040: 726F 6D20 5769 7265 7368 6172 6B20 6F6E  rom Wireshark on
00000050: 2046 7269 2041 7567 2020 3220 3136 3A33   Fri Aug  2 16:3
00000060: 323A 3137 2032 3004 0008 0001 0000 00    2:17 20........

# nokiapcap File Header
00000000: D4C3 B2A1 0200 0400 0000 0000 0000 0000  ................
00000010: 0000 0400 0100 0000                      ........

# nsecpcap File Header
00000000: 4D3C B2A1 0200 0400 0000 0000 0000 0000  M<..............
00000010: 0000 0400 0100 0000                      ........

# pcap File Header
00000000: D4C3 B2A1 0200 0400 0000 0000 0000 0000  ................
00000010: 0000 0400 0100 0000                      ........

# pcapng File Header
00000000: 0A0D 0D0A C800 0000 4D3C 2B1A 0100 0000  ........M<+.....
00000010: FFFF FFFF FFFF FFFF 0200 3700 496E 7465  ..........7.Inte
00000020: 6C28 5229 2043 6F72 6528 544D 2920 6937  l(R) Core(TM) i7
00000030: 2D34 3737 3048 5120 4350 5520 4020 322E  -4770HQ CPU @ 2.
00000040: 3230 4748 7A20 2877 6974 6820 5353 4534  20GHz (with SSE4
00000050: 2E32 2900 0300 2E00 4D61 6320 4F53 2058  .2).....Mac OS X
00000060: 2031 302E 3134 2E35 2C20 6275 696C 6420   10.14.5, build
00000070: 3138 4631 3332 2028 4461 7277 696E 2031  18F132 (Darwin 1
00000080: 382E 362E 3029 0000 0400 3200 4475 6D70  8.6.0)....2.Dump
00000090: 6361 7020 2857 6972 6573 6861 726B 2920  cap (Wireshark)
000000a0: 332E 302E 3320 2876 332E 302E 332D 302D  3.0.3 (v3.0.3-0-
000000b0: 6736 3133 3062 3932 6230 6563 3629 0000  g6130b92b0ec6)..
000000c0: 0000 0000 C800 0000 0100 0000 6800 0000  ............h...
000000d0: 0100 0000 0000 0800 0200 0300 656E 3000  ............en0.
000000e0: 0300 0500 5769 2D46 6900 0000 0900 0100  ....Wi-Fi.......
000000f0: 0600 0000 0C00 2E00 4D61 6320 4F53 2058  ........Mac OS X
00000100: 2031 302E 3134 2E35 2C20 6275 696C 6420   10.14.5, build
00000110: 3138 4631 3332 2028 4461 7277 696E 2031  18F132 (Darwin 1
00000120: 382E 362E 3029 0000 0000 0000 6800 0000  8.6.0)......h...

# rh6_1pcap File Header
00000000: D4C3 B2A1 0200 0400 0000 0000 0000 0000  ................
00000010: 0000 0400 0100 0000                      ........

# snoop File Header
00000000: 736E 6F6F 7000 0000 0000 0002 0000 0004  snoop...........

# suse6_3pcap File Header
00000000: 34CD B2A1 0200 0400 0000 0000 0000 0000  4...............
00000010: 0000 0400 0100 0000                      ........

# visual File Header
00000000: 0556 4E46 0000 0000 0000 0000 0600 FFFF  .VNF............
00000010: 0100 0100 0000 0000 0000 0000 0000 0000  ................
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000040: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000050: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000060: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000070: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000080: 5769 7265 7368 6172 6B20 6669 6C65 0000  Wireshark file..
00000090: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000a0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000b0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
```

## Python: Parse Header/Packet/Footer for any capture

This script will print the header, packet headers, packets, and the footer for any format.

```python
import subprocess as sp
import re
import os

def create_pcap():
    if not os.path.exists("temp.pcapng"):
        sp.call(["tshark", "-w", "temp.pcapng", "-c", "3"])
    return "temp.pcapng"

def get_hexdump(filename):
    output = sp.check_output(["xxd", "-ps", filename], text=True)
    return re.sub(r"\s", "", output)

def get_pcap_header_footer(filename):
    """Get a combination of header/footer from the file."""
    capture_type_text = sp.check_output(["captype", filename], text=True)
    capture_type = re.findall(r"[^:]*: (.*)", capture_type_text)[0]
    sp.call(["tshark", "-r", filename, "-F", capture_type, "-Y", "ipx", "-w", "temp.file"])
    header = get_hexdump("temp.file")
    print(header)
    os.remove("temp.file")
    return header

def get_packets(filename):
    packet_text = sp.check_output(["tshark", "-r", filename, "-x"], text=True)
    packets = packet_text.split("\n\n")  # tshark outputs new packets on a newline
    packets = list(filter(None, packets))
    for i, _ in enumerate(packets):
        # Delete the bytes that are not part of the packet
        packets[i] = re.sub(r"(?:^|\n)\d*  |   .*| ", "", packets[i])

    return packets

def run():
    message = ""
    filename = create_pcap()
    hexdump = get_hexdump(filename)
    pcap_header_footer = get_pcap_header_footer(filename)
    packets = get_packets(filename)
    if 
      pkt0 = re.search(packets[0], hexdump)
    message += "Packet 0:\n" + packets[0] + "\n\n"
    hexdump_remainder = hexdump[pkt0.end():]
    for i, packet in enumerate(packets):
        packet_match = re.search(packet, hexdump_remainder)
        packet_header = hexdump_remainder[:packet_match.start()]
        message += "Packet Header " + str(1) + ":\n" + packet_header + '\n\n'
        message += "Packet " + str(1) + ":\n" + packet + '\n\n'
        hexdump_remainder = hexdump_remainder[packet_match.end():]
    header_search = re.search(hexdump_remainder, pcap_header_footer)
    header = hexdump[:header_search.start()]
    message += "Header+packet0 header:\n" + header + "\n\n" + "Footer:\n", hexdump_remainder
    print(message)

if __name__ == '__main__':
    run()
```

Example output for a 3 packet pcapng file:

<div class="highlight"><pre class="chroma"><code class="language-bash hljs" data-lang="bash" style="overflow-x: auto;white-space: pre-wrap;white-space: -moz-pre-wrap;white-space: -pre-wrap;white-space: -o-pre-wrap;word-wrap: break-word;">Header+packet0 header:
0a0d0d0ac80000004d3c2b1a01000000ffffffffffffffff02003700496e74656c28522920436f726528544d292069372d34373730485120435055204020322e323047487a20287769746820535345342e32290003002e004d6163204f5320582031302e31342e352c206275696c6420313846313332202844617277696e2031382e362e302900000400320044756d70636170202857697265736861726b2920332e302e33202876332e302e332d302d6736313330623932623065633629000000000000c80000000100000068000000010000000000080002000300656e30000300050057692d466900000009000100060000000c002e004d6163204f5320582031302e31342e352c206275696c6420313846313332202844617277696e2031382e362e302900000000000068000000060000007c000000000000006a8f0500a02afb175a0000005a000000

Packet <span class="m">0</span>:
6c96cfd87fe7cc65adda397008004500004c1ad8400031066dc98c52721ac0a801f601bbd53da3d069e9ca0efbcd8018001fe2b400000101080a08d51bb33ea6da3117030300130ac92e61a016dad04ffdd0a697e7b3d9644647

Packet Header <span class="m">1</span>:
00007c0000000600000064000000000000006a8f0500f42afb174200000042000000

Packet <span class="m">1</span>:
cc65adda39706c96cfd87fe708004500003400004000400679b9c0a801f68c52721ad53d01bbca0efbcda3d06a01801007fff31900000101080a3ea7acc208d51bb3

Packet Header <span class="m">2</span>:
0000640000000600000080000000000000006a8f0500ac2cfb175e0000005e000000

Packet <span class="m">2</span>:
cc65adda39706c96cfd87fe7080045000050000040004006799dc0a801f68c52721ad53d01bbca0efbcda3d06a0180180800013f00000101080a3ea7acc208d51bb317030300172525d27b6d058c1236bccb185f56ffc1634643ae8c252e

Footer: 000080000000050000006c000000000000006a8f05003dbafd1701001c00436f756e746572732070726f76696465642062792064756d70636170020008006a8f050056e4f917030008006a8f05000abafd17040008000300000000000000050008000300000000000000000000006c000000</code><span class="copy-to-clipboard" title="Copy to clipboard"></span></pre></div>