
Enterprise Multi-Protocol Routing Challenge (OSPF, RIPv1/v2, & Static)
========================================================================

Author Information:
-------------------
Name: Hammad Zia

Reg No: NETB01-4259 

Domain: Network Administration

Organization: IT-Simplera Solutions

Date of Submission: 17th July, 2026

------------------------------------------------------------------------
Description
------------------------------------------------------------------------
This repository contains the network engineering files, topology maps, 
and documentation for the Week 3 Multi-Protocol Routing Challenge. 
The project implements an enterprise network integrating Multi-Area OSPF, 
RIP v1/v2, and Floating Static Routes across a 9-router infrastructure. 
It features complete route redistribution configurations across protocols and a 
detailed troubleshooting report on core link redundancy failover.

------------------------------------------------------------------------
Repository Layout
------------------------------------------------------------------------
* Report.pdf – Full technical report covering Multi-Area OSPF, RIP metrics, route redistribution, and link failover analysis.
* screenshots/ – Verification captures of routing tables, OSPF neighbor states, and successful multi-protocol ping tests.
* Router Configuration Files/ – Clean CLI running-configurations for Routers 1 through 9 including redistribution and static metrics.
* GNS3 Project/ – Production emulation workspace validating protocol convergence, seed metrics, and backup interfaces.

------------------------------------------------------------------------
Core Modules Covered
------------------------------------------------------------------------
1. Multi-Area OSPF Deployment
   * Segregated topology (Area 0, Area 1) to minimize SPF overhead.
   * Dynamic neighbor adjacencies synchronized through an Area Border Link (R3 to R4).

2. RIP v1/v2 Routing Domain
   * Distance-vector route deployment utilizing hop count metrics for edge segments.
   * Upgraded to classless routing behavior to ensure compatibility with modern VLSM boundaries.

3. Route Redistribution & Metric Mapping
   * Configured cross-protocol route injection on Core Transit Routers (R5 & R6).
   * Mapped OSPF link costs, RIP seed metrics, and subnet tags to maintain loop-free topology traversal.

4. Link Redundancy & Floating Static Routes
   * Primary distribution link routed through Router 5.
   * Floating static backup routes configured with higher Administrative Distance (AD) through Router 6 for automated failover.

------------------------------------------------------------------------
Verification Commands
------------------------------------------------------------------------
* "show ip ospf neighbor" – Verifies FULL neighbor adjacencies and backbone link states.
* "show ip route" – Audits route injection flags such as "O IA" (OSPF Inter-Area) and "R" (RIP).
* "traceroute" (or "tracer") – Tracks exact step-by-step hop interfaces across multi-protocol domains.

------------------------------------------------------------------------
Troubleshooting & Engineering Case Study
------------------------------------------------------------------------
> Case Scenario: R7 to R9 Primary Link Failure]
  During simulated link drop testing between Router 7 and Router 9, packets 
  dropped completely instead of routing along the backup serial link.

> Root Cause Identified:
  An inspection of the routing configurations revealed that the explicit floating 
  static backup path for the R9 target subnet was missing on R7. Without 
  a fallback entry in the routing table, traffic was discarded instantly].

> Resolution Applied:
  Configured the explicit backup static route on Router 7 pointing to the next-hop 
  IP of the backup link[cite: 3]. Running "tracer" confirmed that traffic immediately 
  diverted to the secondary path (Router 6) during unexpected link outages.
========================================================================
