# TCP vs UDP

## TCP

### TCP Datagram

<table class="wikitable" style="text-align: center; border: none;">
<caption>TCP header format (ref: Wikipedia)
</caption>
<tbody><tr>
<th style="min-width:42px; border-bottom:none; border-right:none;"><i>Offset</i>
</th>
<th style="border-left:none;">Octet
</th>
<th colspan="8">0
</th>
<th colspan="8">1
</th>
<th colspan="8">2
</th>
<th colspan="8">3
</th></tr>
<tr>
<th style="min-width: 42px;border-top: none;">Octet
</th>
<th style="min-width: 42px;">Bit
</th>
<th style="min-width:11px;">0
</th>
<th style="min-width:11px;">1
</th>
<th style="min-width:11px;">2
</th>
<th style="min-width:11px;">3
</th>
<th style="min-width:11px;">4
</th>
<th style="min-width:11px;">5
</th>
<th style="min-width:11px;">6
</th>
<th style="min-width:11px;">7
</th>
<th style="min-width:11px;">8
</th>
<th style="min-width:11px;">9
</th>
<th style="min-width:16px;">10
</th>
<th style="min-width:16px;">11
</th>
<th style="min-width:16px;">12
</th>
<th style="min-width:16px;">13
</th>
<th style="min-width:16px;">14
</th>
<th style="min-width:16px;">15
</th>
<th style="min-width:16px;">16
</th>
<th style="min-width:16px;">17
</th>
<th style="min-width:16px;">18
</th>
<th style="min-width:16px;">19
</th>
<th style="min-width:16px;">20
</th>
<th style="min-width:16px;">21
</th>
<th style="min-width:16px;">22
</th>
<th style="min-width:16px;">23
</th>
<th style="min-width:16px;">24
</th>
<th style="min-width:16px;">25
</th>
<th style="min-width:16px;">26
</th>
<th style="min-width:16px;">27
</th>
<th style="min-width:16px;">28
</th>
<th style="min-width:16px;">29
</th>
<th style="min-width:16px;">30
</th>
<th style="min-width:16px;">31
</th></tr>
<tr>
<th style="width:35px;">0
</th>
<th style="width:30px;">0
</th>
<td colspan="16"><i>Source Port</i>
</td>
<td colspan="16"><i>Destination Port</i>
</td></tr>
<tr>
<th style="width:35px;">4
</th>
<th style="width:30px;">32
</th>
<td colspan="32"><i>Sequence Number</i>
</td></tr>
<tr>
<th style="width:35px;">8
</th>
<th style="width:30px;">64
</th>
<td colspan="32"><i>Acknowledgement Number (meaningful when ACK bit set)</i>
</td></tr>
<tr>
<th style="width:35px;">12
</th>
<th style="width:30px;">96
</th>
<td colspan="4"><i>Data Offset</i>
</td>
<td colspan="4"><i>Reserved</i>
</td>
<td><i><style data-mw-deduplicate="TemplateStyles:r1231500821">@supports(writing-mode:vertical-lr){.mw-parser-output .ts-vertical-text{letter-spacing:-0.12em;line-height:1em;text-orientation:upright;writing-mode:vertical-lr;width:1em}}</style><span class="ts-vertical-text" style="">CWR</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">ECE</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">URG</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">ACK</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">PSH</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">RST</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">SYN</span></i>
</td>
<td><i><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r1231500821"><span class="ts-vertical-text" style="">FIN</span></i>
</td>
<td colspan="16"><i>Window</i>
</td></tr>
<tr>
<th style="width:35px;">16
</th>
<th style="width:30px;">128
</th>
<td colspan="16">Checksum
</td>
<td colspan="16"><i>Urgent Pointer (meaningful when URG bit set)</i>
</td></tr>
<tr>
<th style="width:35px;">20
</th>
<th style="width:30px;">160
</th>
<td colspan="32" rowspan="3" style="background: linen;"><i>(Options) If present, Data Offset will be greater than 5.<br>Padded with zeroes to a multiple of 32 bits, since Data Offset counts words of 4 octets.</i>
</td></tr>
<tr>
<th>⋮
</th>
<th>⋮
</th></tr>
<tr>
<th>56
</th>
<th>448
</th></tr>
<tr>
<th style="width:35px;">60
</th>
<th style="width:30px;">480
</th>
<td colspan="32" rowspan="3" style="background: mistyrose;"><i>Data</i>
</td></tr>
<tr>
<th>64
</th>
<th>512
</th></tr>
<tr>
<th>⋮
</th>
<th>⋮
</th></tr></tbody></table>

- From [Wikipedia](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)

### TCP Header
<table>
  <tr>
    <th>Field</th>
    <th>Bits</th>
    <th></th>
  </tr>
  <tr>
    <td>Sequence Number</td>
    <td>32</td>
    <td>
      <p>If SYN=1</p>
      <ul>
        <li>initial sequence number (random)</li>
      </ul>
      <p>If SYN=0</p>
      <ul>
        <li>first actual data: ISN+1</li>
        <li>after n bytes are sent: ISN+1+n</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Acknowledgement Number</td>
    <td>32</td>
    <td>
      <p>If ACK=1</p>
      <ul>
        <li>ISN+1</li>
      </ul>
      <p>If ACK=0</p>
      <ul>
        <li>ignored</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Data Offset</td>
    <td>4</td>
    <td>
      <ul>
        <li>Size of the header in 32-bit words</li>
        <li>Options field is variable</li>
      </ul>
    </td>
  </tr>
</table>

### TCP Handshake
![handshake](./assets/tcp-udp-handshake.png)
- From [GeeksForGeeks](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/)


1\. SYN
-  client sends `seq=x`, `SYN`

2\. SYN + ACK
- server sends `seq=y`, `ack=x+1`, `SYN`, `ACK`

3\. ACK
- client sends `ack=y+1`, `ACK`


### TCP Sliding Window
![window](./assets/tcp-udp-window.jpg)
- From [GeeksForGeeks](https://www.geeksforgeeks.org/sliding-window-protocol-set-3-selective-repeat/)

How to notify the packets are not arrived
1. Timeout
2. Duplicate ACKs

### TCP Graceful Connection Release
![close](./assets/tcp-udp-release.png)
- From [GeeksForGeeks](https://www.geeksforgeeks.org/tcp-connection-termination/)

1. FIN
2. ACK
3. FIN
4. ACK



## UDP

### UDP Datagram
<table class="wikitable" style="text-align: center; border: none;">
<caption>UDP header format
</caption>
<tbody><tr>
<th style="min-width:42px; border-bottom:none; border-right:none;"><i>Offset</i>
</th>
<th style="border-left:none;">Octet
</th>
<th colspan="8">0
</th>
<th colspan="8">1
</th>
<th colspan="8">2
</th>
<th colspan="8">3
</th></tr>
<tr>
<th style="min-width: 42px;border-top: none;">Octet
</th>
<th style="min-width: 42px;">Bit
</th>
<th style="min-width:11px;">0
</th>
<th style="min-width:11px;">1
</th>
<th style="min-width:11px;">2
</th>
<th style="min-width:11px;">3
</th>
<th style="min-width:11px;">4
</th>
<th style="min-width:11px;">5
</th>
<th style="min-width:11px;">6
</th>
<th style="min-width:11px;">7
</th>
<th style="min-width:11px;">8
</th>
<th style="min-width:11px;">9
</th>
<th style="min-width:16px;">10
</th>
<th style="min-width:16px;">11
</th>
<th style="min-width:16px;">12
</th>
<th style="min-width:16px;">13
</th>
<th style="min-width:16px;">14
</th>
<th style="min-width:16px;">15
</th>
<th style="min-width:16px;">16
</th>
<th style="min-width:16px;">17
</th>
<th style="min-width:16px;">18
</th>
<th style="min-width:16px;">19
</th>
<th style="min-width:16px;">20
</th>
<th style="min-width:16px;">21
</th>
<th style="min-width:16px;">22
</th>
<th style="min-width:16px;">23
</th>
<th style="min-width:16px;">24
</th>
<th style="min-width:16px;">25
</th>
<th style="min-width:16px;">26
</th>
<th style="min-width:16px;">27
</th>
<th style="min-width:16px;">28
</th>
<th style="min-width:16px;">29
</th>
<th style="min-width:16px;">30
</th>
<th style="min-width:16px;">31
</th></tr>
<tr>
<th style="width:35px;">0
</th>
<th style="width:30px;">0
</th>
<td colspan="16" style="background: lavender;"><i>Source Port</i>
</td>
<td colspan="16"><i>Destination Port</i>
</td></tr>
<tr>
<th style="width:35px;">4
</th>
<th style="width:30px;">32
</th>
<td colspan="16"><i>Length</i>
</td>
<td colspan="16" style="background: lavender;"><i>Checksum</i>
</td></tr>
<tr>
<th style="width:35px;">8
</th>
<th style="width:30px;">64
</th>
<td colspan="32" rowspan="3" style="background: mistyrose;"><i>Data</i>
</td></tr>
<tr>
<th>12
</th>
<th>96
</th></tr>
<tr>
<th>⋮
</th>
<th>⋮
</th></tr></tbody></table>

- From [Wikipedia](https://en.wikipedia.org/wiki/User_Datagram_Protocol)


### UDP Header

<table>
  <tr>
    <th>Field</th>
    <th>Bits</th>
    <th></th>
  </tr>
  <tr>
    <td>Source port</td>
    <td>16</td>
    <td>
      <ul>
        <li>server or client</li>
        <li>well-known: 0-1023</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Destination port</td>
    <td>16</td>
    <td>
      <ul>
        <li>server or client</li>
        <li>well-known: 0-1023</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Length</td>
    <td>16</td>
    <td>
      <ul>
        <li>length in bytes of the UDP datagram (header + data)</li>
        <li>minimum = 8</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Checksum</td>
    <td>16</td>
    <td>
      <ul>
        <li>IPv4: optional</li>
        <li>IPv6: mandatory</li>
      </ul>
    </td>
  </tr>
</table>

## TCP vs UDP

<table>
  <tr>
    <th>TCP</th>
    <th>UDP</th>
  </tr>
  <tr>
    <td>Reliable</td>
    <td>Unreliable</td>
  </tr>
  <tr>
    <td>Ordered</td>
    <td>Not ordered</td>
  </tr>
  <tr>
    <td>Heavyweight</td>
    <td>Lightweight</td>
  </tr>
  <tr>
    <td>Streaming</td>
    <td>
      <p>
        No congestion control<br>
        Broadcasts<br>
        Multicast
      </p>
    </td>
  </tr>
</table>

## Application

<table>
  <tr>
    <th>TCP</th>
    <th>UDP</th>
  </tr>
  <tr>
    <td>
      <ul>
        <li>World Wide Web (WWW)</li>
        <li>email</li>
        <li>File Transfer Protocol (FTP)</li>
        <li>Secure Shell (SSH)</li>
        <li>Peer-to-peer file sharing</li>
        <li>Streaming media</li>
        <li>VoIP</li>
        <li>Real-time Transport Protocol (RTP)</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>Domain Name System (DNS)</li>
        <li>Simple Network Management Protocol (SNMP)</li>
        <li>Routing Information Protocol (RIP)</li>
        <li>voice, video, audio</li>
        <li>QUIC, HTTP/3 (RUDP)</li>
      </ul>
    </td>
  </tr>
</table>
