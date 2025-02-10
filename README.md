<h1>CCNA Subnetting and Static Routing Lab</h1>

<h2>Description</h2>
<p>This lab demonstrates subnetting using Variable Length Subnet Masks (VLSM) and configuring static routes to connect multiple LANs and a point-to-point link. The network consists of multiple subnets, each with varying host requirements, and uses Cisco routers to ensure inter-network communication.</p>

<h2>Technologies and Tools Used</h2>
<ul>
  <li><b>Cisco Packet Tracer</b> - For network simulation.</li>
  <li><b>Cisco Routers and Switches</b> - Virtual devices in Packet Tracer.</li>
  <li><b>PC Command Line Interface (CLI)</b> - For connectivity tests using <code>ping</code>.</li>
</ul>

<h2>Network Diagram</h2>
<p align="center">
  <img src="images/topology.png" alt="Network Topology"/>
</p>

<h2>Subnetting Calculations</h2>
<table align="center" border="1">
  <tr>
    <th>Subnet</th>
    <th>Prefix Length</th>
    <th>Network Address</th>
    <th>Broadcast Address</th>
    <th>Usable Host Range</th>
  </tr>
  <tr>
    <td>LAN2</td>
    <td>/25</td>
    <td>192.168.5.0</td>
    <td>192.168.5.127</td>
    <td>192.168.5.1 - 192.168.5.126</td>
  </tr>
  <tr>
    <td>LAN1</td>
    <td>/26</td>
    <td>192.168.5.128</td>
    <td>192.168.5.191</td>
    <td>192.168.5.129 - 192.168.5.190</td>
  </tr>
  <tr>
    <td>LAN3</td>
    <td>/28</td>
    <td>192.168.5.192</td>
    <td>192.168.5.207</td>
    <td>192.168.5.193 - 192.168.5.206</td>
  </tr>
  <tr>
    <td>LAN4</td>
    <td>/28</td>
    <td>192.168.5.208</td>
    <td>192.168.5.223</td>
    <td>192.168.5.209 - 192.168.5.222</td>
  </tr>
  <tr>
    <td>P2P</td>
    <td>/30</td>
    <td>192.168.5.224</td>
    <td>192.168.5.227</td>
    <td>192.168.5.225 - 192.168.5.226</td>
  </tr>
</table>

<h2>Program Walk-through:</h2>

<p align="center">
Configure <b>Router 1</b>: <br/>
<img src="images/router1-config.png" alt="Router 1 Configuration"/>
</p>

<pre>
enable
configure terminal

! Configure LAN2 (G0/1)
interface g0/1
ip address 192.168.5.126 255.255.255.128
no shutdown

! Configure LAN1 (G0/0)
interface g0/0
ip address 192.168.5.190 255.255.255.192
no shutdown

! Configure Point-to-Point Link (G0/0/0)
interface g0/0/0
ip address 192.168.5.225 255.255.255.252
no shutdown

! Configure Static Routes
ip route 192.168.5.192 255.255.255.240 192.168.5.226
ip route 192.168.5.208 255.255.255.240 192.168.5.226
</pre>

<p align="center">
Configure <b>Router 2</b>: <br/>
<img src="images/router2-config.png" alt="Router 2 Configuration"/>
</p>

<pre>
enable
configure terminal

! Configure LAN3 (G0/0)
interface g0/0
ip address 192.168.5.206 255.255.255.240
no shutdown

! Configure LAN4 (G0/1)
interface g0/1
ip address 192.168.5.222 255.255.255.240
no shutdown

! Configure Point-to-Point Link (G0/0/0)
interface g0/0/0
ip address 192.168.5.226 255.255.255.252
no shutdown

! Configure Static Routes
ip route 192.168.5.128 255.255.255.192 192.168.5.225
ip route 192.168.5.0 255.255.255.128 192.168.5.225
</pre>

<h2>PC Configurations</h2>

<p align="center">
<img src="images/pc-config.png" alt="PC Configurations"/>
</p>

<pre>
PC1 (LAN1)
Default Gateway: 192.168.5.190
IP Address: 192.168.5.129
Subnet Mask: 255.255.255.192

PC2 (LAN2)
Default Gateway: 192.168.5.126
IP Address: 192.168.5.1
Subnet Mask: 255.255.255.128

PC3 (LAN3)
Default Gateway: 192.168.5.206
IP Address: 192.168.5.193
Subnet Mask: 255.255.255.240

PC4 (LAN4)
Default Gateway: 192.168.5.222
IP Address: 192.168.5.209
Subnet Mask: 255.255.255.240
</pre>

<h2>Testing Connectivity</h2>

<p align="center">
Testing <b>ping</b> from PC1 to PC4: <br/>
<img src="images/ping-test.png" alt="Ping Test Results"/>
</p>

<pre>
PC1> ping 192.168.5.209

Reply from 192.168.5.209: bytes=32 time<1ms TTL=64
</pre>

<h2>Lessons Learned</h2>
<ul>
  <li>Improved understanding of VLSM and its importance in efficient IP address allocation.</li>
  <li>Gained hands-on experience with configuring static routes.</li>
  <li>Learned how to verify connectivity using CLI tools like <code>ping</code> and <code>traceroute</code>.</li>
</ul>
