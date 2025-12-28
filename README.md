<h1>🌐 BGP Lab</h1>

<h2>Project Overview</h2>
<p>This lab is designed to gain a practical and conceptual understanding of <strong>BGP (Border Gateway Protocol)</strong>, the foundational protocol used to exchange routing information between autonomous systems (AS) on the Internet.</p>
<p>Even though many enterprises rely on internal routing protocols like OSPF or EIGRP for intra-domain routing, BGP is the protocol that connects different networks and ISPs securely and efficiently. Learning BGP teaches how routing policies are applied, how prefixes are advertised and filtered, and how autonomous systems interact which is an essential skill for any network engineer working in enterprise or ISP environments.</p>

<h2>Objective</h2>
<ul>
    <li>Understand how BGP establishes routing between autonomous systems.</li>
    <li>Configure eBGP peering across WAN links.</li>
    <li>Advertise and filter routes using BGP policies and prefix lists.</li>
    <li>Observe path selection and routing updates in a multi-AS environment.</li>
    <li>Gain experience with Cisco IOS BGP configuration and troubleshooting.</li>
</ul>

<h2>IP Addressing & Subnetting</h2>
<pre>
| Network        | IP Range        | Subnet Mask      | Description                          |
|--------------- |---------------- |----------------- |--------------------------------------|
| Site-A LAN     | 192.168.10.0/24 | 255.255.255.0    | Site-A internal network              |
| Site-A WAN     | 203.0.113.0/30  | 255.255.255.252  | WAN link to Site-C (Site-C = .1)     |
| Site-B LAN     | 192.168.20.0/24 | 255.255.255.0    | Site-B internal network              |
| Site-B WAN     | 192.0.2.0/30    | 255.255.255.252  | WAN link to Site-C (Site-C = .1)     |
| Site-C WAN-1   | 203.0.113.1/30  | 255.255.255.252  | WAN interface to Site-A              |
| Site-C WAN-2   | 192.0.2.1/30    | 255.255.255.252  | WAN interface to Site-B              |
</pre>

<img width="1407" height="444" alt="BGP full pic" src="https://github.com/user-attachments/assets/05fb5fab-215e-4467-8968-70e3c74f2688" />

<div class="img-caption">High-level topology showing Site-A, ISP, and Site-B with BGP peerings.</div>

<h2>How the BGP Lab Works</h2>
<p>This lab demonstrates how BGP connects multiple sites in a hub-and-spoke topology and shares routing information:</p>
<ul>
    <li><strong>Forming neighbor sessions:</strong> Each router establishes a BGP session with its peers (neighbors) over TCP port 179 to exchange routing information.</li>
    <li><strong>Path-vector protocol:</strong> BGP is a path-vector protocol, meaning it chooses routes based on policies and path attributes (like AS path) rather than the shortest path.</li>
    <li><strong>Advertising networks:</strong> Each site announces the networks it can reach (its LAN and WAN subnets). BGP uses this information to determine the best path for traffic.</li>
    <li><strong>Applying routing policies:</strong> You can control which routes are shared or accepted using prefix-lists, route-maps, or filters.</li>
    <li><strong>Forwarding traffic:</strong> Once routes are learned, traffic between Site-A and Site-B flows through Site-C following the best path as determined by BGP policies and path selection rules.</li>
    <li><strong>Use case:</strong> BGP is mainly used for ISP connections, external WANs, and multi-AS networks where scalability, policy control, and inter-AS communication are needed.</li>
    <li><strong>Convergence:</strong> BGP convergence is slower than internal protocols like OSPF, because route updates propagate through neighbors rather than the full network topology.</li>
</ul>


<h2>Testing & Validation</h2>


<h3>2. Ping & Tracert Between Sites</h3>
<img width="833" height="629" alt="ping and tracert" src="https://github.com/user-attachments/assets/74f66309-8d3b-42e4-90aa-2d17ced4a9f8" />
<div class="img-caption">Testing connectivity between Site-A and Site-B LANs. Successful ping confirms correct route propagation via BGP.</div>

<h3>3. Show BGP Routes</h3>
<img width="826" height="628" alt="Show IP BGP" src="https://github.com/user-attachments/assets/c3e7a8af-7a46-4e6b-b37f-6a9fbff31c98" />
<div class="img-caption">Inspecting advertised prefixes, AS paths, and best paths using <code>show ip bgp</code>.</div>

<h3>4. Show Routing Table</h3>
<img width="727" height="520" alt="Routing Table - SITE C" src="https://github.com/user-attachments/assets/05e9b98f-ee8e-4b58-b2e9-5817ce23ccb9" />
<div class="img-caption">Confirmation that BGP-learned prefixes are in the routing table and traffic will be forwarded accordingly.</div>
