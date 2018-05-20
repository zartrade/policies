# 1. Introduction

Shape Software, LLC ("Shape Software") is committed to ensuring the confidentiality, privacy, integrity, and availability of all electronic protected health information (ePHI) it receives, maintains, processes and/or transmits on behalf of its Customers. As providers of compliant, hosted infrastructure used by health technology vendors, developers, designers, agencies, custom development shops, and enterprises, Shape Software strives to maintain compliance, proactively address information security, mitigate risk for its Customers, and assure known breaches are completely and effectively communicated in a timely manner. The following documents address core policies used by Shape Software to maintain compliance and assure the proper protections of infrastructure used to store, process, and transmit ePHI for Shape Software Customers.

Shape Software provides secure and compliant cloud-based software. This hosted software falls into two broad categories: 1) **Platform as a Service (PaaS)** and 2) **Platform Add-ons**. These Categories are cited throughout polices as Customers in each category inherit different policies, procedures, and obligations from Shape Software.

## 1.1 Platform as a Service (PaaS)

PaaS Customers utilize hosted software and infrastructure from Shape Software to deploy, host, and scale custom developed applications and configured databases. These customers are deployed into compliant containers running on systems secured and managed by Shape Software. Shape Software does not have insight or access into application level data of PaaS Customers and, as such, does not have the ability to secure or manage risk associated with application level vulnerabilities and security weaknesses. Shape Software makes every effort to reduce the risk of unauthorized disclosure, access, and/or breach of PaaS Customer data through network (firewalls, dedicated IP spaces, etc) and server settings (encryption at rest and in transit, OSSEC throughout the Platform, etc).

## 1.2 Compliance Inheritance

Shape Software provides compliant hosted software infrastructure for its Customers. Shape Software has been through a HIPAA compliance audit by a national third-party compliance firm to validate and map organizational policies and technical controls to HIPAA rules. Shape Software's company policies, procedures, and technologies are HITRUST Certified. Shape Software's service offerings are available on Turnkey Internet Services Dedicated Hosted Solutions.

Shape Software signs Business Associate Agreements (BAAs) with its Customers. These BAAs outline Shape Software obligations and Customer obligations, as well as liability in the case of a breach. In providing infrastructure and managing security configurations that are a part of the technology requirements that exist in HIPAA and HITRUST, as well as future compliance frameworks, Shape Software manages various aspects of compliance for Customers. The aspects of compliance that Shape Software manages for Customers are inherited by Customers, and Shape Software assumes the risk associated with those aspects of compliance. In doing so, Shape Software helps Customers achieve and maintain compliance, as well as mitigates Customers risk.

Shape Software does not act as a covered entity. When Shape Software does operate as a business associate (not a subcontractor), Shape Software does not interface with users to obtain or provide access to ePHI. Access to ePHI is through our customers applications.

Certain aspects of compliance cannot be inherited. Because of this, Shape Software Customers, in order to achieve full compliance or HITRUST Certification, must implement certain organizational policies. These policies and aspects of compliance fall outside of the services and obligations of Shape Software.

Mappings of HIPAA Rules to Shape Software controls and a mapping of what Rules are inherited by Customers, both Platform Customers and Add-on Customers, are covered in [§2](#2.-hipaa-inheritance).

## 1.3 Shape Software Organizational Concepts

Shape Software uses Datica Health, Inc ("Datica") to meet and exceed HIPAA's technical requirements. With Datica, we're not only HIPAA compliant but also HITRUST CSF Certified.

The physical infrastructure environment is hosted at [Turnkey Internet](https://turnkeyinternet.net/). The network components and supporting network infrastructure are contained within the Turnkey Internet and managed by Turnkey Internet. Shape Software does not have physical access into the network components. The Shape Software environment consists of NGinx web servers; Percona database servers; Ubuntu Linux monitoring servers and OSSEC IDS services.

Within the Shape Software Platform on Turnkey Internet Hosted Servers, all data transmission is encrypted and network traffic is contained for all database access on internet private network and not public facing; this applies to all servers. Shape Software assumes all data *may* contain ePHI, even though our Risk Assessment does not indicate this is the case, and provides appropriate protections based on that assumption.

In the case of PaaS Customers, it is the responsibility of the Customer to restrict, secure, and assure the privacy of all ePHI data at the Application Level, as this is not under the control or purview of Shape Software.

The segmentation strategies employed by Shape Software effectively create RFC 1918, or dedicated, private segmented and separated networks and IP spaces, for each PaaS Customer and for Platform Add-ons.

Additionally, IPtables is used on each server for logical segmentation. IPtables is configured to restrict access to only justified ports and protocols. Shape Software has implemented strict logical access controls so that only authorized personnel are given access to the internal management servers.

The SSH server, nginx web server, and application servers are externally facing and accessible via the Internet. The database servers, where the ePHI resides, are located on the internal Shape Software network and can only be accessed through a SSH connection using SSH Private/Public Key Encryption. Access to the internal database is restricted to a limited number of personnel and strictly controlled to only those personnel with a business-justified reason. Remote access to internal servers is not accessible except through authorized SSH Access.

