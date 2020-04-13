---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Installation Guide
description: Download and begin using content.

# Author box
#author:
#    title: About Author
#    title_url: '#'
#    external_url: true
#    description: Author description

# Micro navigation
micro_nav: true

# Page navigation
#page_nav:
#    prev:
#        content: Previous page
#        url: '#'
#    next:
#        content: Next page
#        url: '#'
---

# Installation

## Upstream Content

### GitHub Releases
Download pre-built releases, including associated release source code, via the GitHub Releases. Upstream releases are performed approximately every three months.

[https://github.com/ComplianceAsCode/content/releases](https://github.com/ComplianceAsCode/content/releases)


### COPR
Copr is a Fedora project to help make building and managing package repositories easy. ComplianceAsCode's COPR repository provides unofficial builds of the latest tools and content, including those from the broader open source SCAP ecosystem, such as ``openscap``, ``scap-workbench``, and ``openscap-daemon``. The packages are suitable for use on RHEL, CentOS, and Scientific Linux.

The COPR repository is located at [https://copr.fedorainfracloud.org/coprs/openscapmaint/openscap-latest/](https://copr.fedorainfracloud.org/coprs/openscapmaint/openscap-latest/)

## Downstream Packages
Multiple Linux distributions package ComplianceAsCode content natively. These packages generally provide the most stable experience, and are often supported by your Linux vendor.

Some distributions still package ComplianceAsCode by its previous name, *SCAP Security Guide*. As a result packages are often named ``scap-security-guide``.

### Fedora, Red Hat Enterprise Linux, and CentOS

``
$ sudo yum install scap-security-guide
``

### Debian and Ubuntu
For Debian guides:

``$ sudo apt install ssg-debian``

For Debian-based Distributions, such as Ubuntu:

``$ sudo apt install ssg-debderived``

Non-Debian operating system content, eg to evaluate a RHEL container on a Debian host:
``$ sudo install ssg-nondebian``

Non-Debian application content, such as FireFox and JBoss:
``$ sudo install ssg-application``

# Usage
The following guidance assumes ComplianceAsCode is installed into a standard system-wide location, such as ``/usr/share/xml/scap/ssg/content`` or ``/usr/share/xml/scap/ComplianceAsCode/``.

## Running a Configuration Evaluation

### OpenSCAP
OpenSCAP, delivered in many Linux distributions as the ``oscap`` tool, provides a command line interface to performing configuration and CVE scanning.

To list available compliance profiles:
```bash
$ oscap info /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml
```

An example CLI command to run a scan:

```bash
$ sudo oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_rht-ccp \
--results-arf arf.xml \
--report report.html \
--oval-results /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

After evaluation the ``arf.xml`` file will contain all results in a reusable *Results DataStream* format. ``report.html`` will contain a human readable report that can be opened in a browser. 

Refer to the [OpenSCAP User Manual](https://static.open-scap.org/openscap-1.2/oscap_user_manual.html) for more information.

### SCAP Workbench
SCAP Workbench is a graphical user interface for SCAP evaluation and customization. It is suitable for scanning a single machine, either local or remote (via SSH), and for tailoring SCAP content. Recent versions of SCAP Workbench have ComplianceAsCode integration and will automatically offer profiles when the application is started.

See the [SCAP Workbench User Manual](https://static.open-scap.org/scap-workbench-1.1/) for more information.

### oscap-ssh Tool
``oscap-ssh`` comes bundled with OpenSCAL 1.2.3 and later. It allows scanning a remote machine via SSH with an interface resembling the ``oscap`` tool.

The following command evaluates a machine with the IP address of ``192.168.1.123`` with content stored on the local machine. Note that ``oscap`` has to be installed on the remote machine, however the ComplianceAsCode content doesn't need to be.

```bash
$ oscap-ssh root@192.168.1.123 22 \
xccdf eval --profile xccdf_org.ssgproject.content_profile_usgcb-rhel6-server \
--results-arf arf.xml \
--report report.html \
/usr/share/xml/scap/ssg/content/ssg-rhel6-ds.xml
```

## Remediation

### Ansible Playbooks
To see a list of available Ansible Playbooks:

```bash
$ ls /usr/share/scap-security-guide/ansible/
...
rhel6-playbook-standard.yml
rhel6-playbook-stig-rhel6-server-upstream.yml
rhel6-playbook-usgcb-rhel6-server.yml
rhel7-playbook-C2S.yml
rhel7-playbook-cjis-rhel7-server.yml
rhel7-playbook-common.yml
rhel7-playbook-docker-host.yml
rhel7-playbook-cui.yml
...
```

To apply the playbook on your local machine:

```bash
$ ansible-playbook -i "localhost," \
-c local /usr/share/scap-security-guide/ansible/rhel7-playbook-rht-ccp.yml
```

Each of the Ansible Playbooks contain instructions on how to deploy them. Here is a snippet of the instructions:

```
...
# This file was generated by OpenSCAP 1.2.16 using:
#   $ oscap xccdf generate fix --profile rht-ccp --template urn:xccdf:fix:script:ansible sds.xml
#
# This script is generated from an OpenSCAP profile without preliminary evaluation.
# It attempts to fix every selected rule, even if the system is already compliant.
#
# How to apply this remediation role:
# $ ansible-playbook -i "192.168.1.155," playbook.yml
# $ ansible-playbook -i inventory.ini playbook.yml
...
```

### Bash Scripts
To see a list of available Bash scripts:

```bash
$ ls /usr/share/scap-security-guide/bash/
...
rhel7-script-hipaa.sh
rhel7-script-ospp.sh
rhel7-script-pci-dss.sh
...
```