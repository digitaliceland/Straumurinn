# Security Server Installation Guide

**X-ROAD 6**

Version: 0.1  
Doc. ID: IG-SS

---


## Version history

 Date       | Version | Description                                                     | Author
 ---------- | ------- | --------------------------------------------------------------- | --------------------
 12.09.2019 | 0.1     | Initial version                                                 | Gudvardur Olafsson

## Table of Contents

<!-- toc -->

- [License](#license)
- [1 Introduction](#1-introduction)
  * [1.1 Target Audience](#11-target-audience)
  * [1.2 Terms and abbreviations](#12-terms-and-abbreviations)
  * [1.3 References](#13-references)
- [2 Installation](#2-installation)
  * [2.1 Supported Platforms](#21-supported-platforms)
  * [2.2 Reference Data](#22-reference-ata)
  * [2.3 Network Diagram](#23-network-diagram)
  * [2.4 Requirements for the Security Server](24-requirements-for-the-security-server)
<!-- tocstop -->

## 1 Introduction


### 1.1 Target Audience

The intended audience of this Installation Guide are X-Road Security server system administrators responsible for installing and using X-Road software. The daily operation and maintenance of the security server is covered by its User Guide \[[UG-SS](#Ref_UG-SS)\].

The document is intended for readers with a moderate knowledge of Linux server management, computer networks, and the X-Road working principles.

### 1.2 Terms and abbreviations

See X-Road terms and abbreviations documentation \[[TA-TERMS](#Ref_TERMS)\].

### 1.3 References

1.  <a id="Ref_UG-SS" class="anchor"></a>\[UG-SS\] X-Road 6. Security Server User Guide. Document ID: [UG-SS](https://github.com/nordic-institute/X-Road/blob/develop/doc/Manuals/ug-ss_x-road_6_security_server_user_guide.md)

2.  <a id="Ref_TERMS" class="anchor"></a>\[TA-TERMS\] X-Road Terms and Abbreviations. Document ID: [TA-TERMS](https://github.com/nordic-institute/X-Road/blob/develop/doc/terms_x-road_docs.md).

## 2 Installation


### 2.1 Supported Platforms

The security server runs on the following platforms:

* Red Hat Enterprise Linux 7.3 (RHEL7) or newer operating system on a 64-bit platform. The security server software is distributed as .rpm packages through the official X-Road repository at https://artifactory.niis.org/xroad-release-rpm/
* Ubuntu Server 14.04 and 18.04 Long-Term Support (LTS) operating system. See [IG-SS](ig-ss_x-road_v6_security_server_installation_guide.md) for more information.

*Note:* If run in production environment RHEL7 install with subscription is recommenend by Icelandic X-Road Operators


### 2.2 Reference Data

*Note*: The information in empty cells should be determined before the server’s installation, by the person performing the installation.

**Caution**: Data necessary for the functioning of the operating system is not included.

**Ref** |                                         | **Explanation**
 ------ | --------------------------------------- | ----------------------------------------------------------
 1.0    | RHEL7 (v7.3 or newer), 64-bit<br>2 CPU, 4 GB RAM, 10 GB free disk space | Minimum requirements
 1.1    | https://artifactory.niis.org/xroad-release-rpm               | X-Road package repository
 1.2    | https://artifactory.niis.org/api/gpg/key/public | The repository key
 1.3    |                                         | Account name in the user interface
 1.4    | TCP 5500                                | Port for inbound connections (from the external network to the security server)<br> Message exchange between security servers
 &nbsp; | TCP 5577                                | Port for inbound connections (from the external network to the security server)<br> Querying of OCSP responses between security servers
 &nbsp; | TCP 9011                                | Port for inbound connections (from the external network to the security server)<br> Operational data monitoring daemon JMX listening port
  &nbsp; | TCP 9999                                | Port for inbound connections (from the external network to the security server)<br> Environmental monitoring daemon JMX listening port
 1.5  | TCP 5500                                  | Ports for outbound connections (from the security server to the external network)<br> Message exchange between security servers
 &nbsp; | TCP 5577                                | Ports for outbound connections (from the security server to the external network)<br> Querying of OCSP responses between security servers
 &nbsp; | TCP 4001                                | Ports for outbound connections (from the security server to the external network)<br> Communication with the central server
 &nbsp; | TCP 2080                                | Ports for outbound connections (from the security server to the internal network)<br> Message exchange between security server and operational data monitoring daemon (by default on localhost)
 &nbsp; | TCP 80                                  | Ports for outbound connections (from the security server to the external network)<br> Downloading global configuration
 &nbsp; | TCP 80,443                              | Ports for outbound connections (from the security server to the external network)<br> Most common OCSP and time-stamping services
 1.6  | TCP 4000                                  | User interface (local network)
 1.7  | TCP 8080                                  | Information system access points (in the local network)<br> Connections from information systems
 &nbsp; | TCP 8443                                | Information system access points (in the local network)<br> Connections from information systems
 1.8  |                                           | Security server internal IP address(es) and hostname(s)
 1.9  |                                           | Security server public IP address, NAT address
 1.10 | x::y / x.x.x.x                            | Monitoring Security Server IP in IS instance
 &nbsp; | x::y / x.x.x.x                           | Monitoring Security Server IP in IS-test instance
 &nbsp; | x::y / x.x.x.x                           | Monitoring Security Server IP in IS-dev instance

### 2.3 Network Diagram

The following network diagram is an example of a simple stand-alone Security Server setup. Attention should be paid when configuring the firewall of your Security Server, as misconfigurations (e.g. exposing port 80/tcp to the public internet) can leave your server vulnerable.

Allowing incoming connections from the Monitoring Security Server on ports 5500/tcp and 5577/tcp (reference data: 1.10) is necessary for the X-Road Center to be able to monitor the ecosystem and provide statistics and support for Members.

Caution: The enabling of auxiliary services which are necessary for the functioning and management of the operating system (such as DNS, NTP, and SSH) stay outside the scope of this guide.

![Network Drawing](../images/ig-ss_network_diagram.png)

**IS IP Address Whitelist** | **IS - Production** | **IS test** | **IS dev**
 --------------------------- | --------------------|-------------|---------------
 Central Server | x::y / x.x.x.x | x::y / x.x.x.x | x::y / x.x.x.x
 Central Monitoring Server | x::y / x.x.x.x | x::y / x.x.x.x | x::y / x.x.x.x
 Managment Security Server | x::y / x.x.x.x | x::y / x.x.x.x | x::y / x.x.x.x

### 2.4 Requirements for the Security Server

Minimum recommended hardware parameters:

-   the server’s hardware (motherboard, CPU, network interface cards, storage system) must be supported by RHEL7 in general;

-   a 64-bit dual-core Intel, AMD or compatible CPU; AES instruction set support is highly recommended;

-   2 CPU;

-   4 GB RAM;

-   10 GB free disk space (OS partition), 20-40 GB free disk space (`/var` partition);

-   a 100 Mbps network interface card.

Requirements to software and settings:

-   an installed and configured RHEL7 (v7.3 or newer) x86-64 operating system;

-   if the security server is separated from other networks by a firewall and/or NAT, the necessary connections to and from the security server are allowed (**reference data: 1.4; 1.5; 1.6; 1.7**). The enabling of auxiliary services which are necessary for the functioning and management of the operating system (such as DNS, NTP, and SSH) stay outside the scope of this guide;

-   if the security server has a private IP address, a corresponding NAT record must be created in the firewall (**reference data: 1.9**).