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

# Upstream Releases

## GitHub Releases
Download pre-built releases, including associated release source code, via the GitHub Releases. Upstream releases are performed approximately every three months.

[https://github.com/ComplianceAsCode/content/releases](https://github.com/ComplianceAsCode/content/releases)


## COPR
Copr is a Fedora project to help make building and managing package repositories easy. ComplianceAsCode's COPR repository provides unofficial builds of the latest tools and content, including those from the broader open source SCAP ecosystem, such as ``openscap``, ``scap-workbench``, and ``openscap-daemon``. The packages are suitable for use on RHEL, CentOS, and Scientific Linux.

The COPR repository is located at [https://copr.fedorainfracloud.org/coprs/openscapmaint/openscap-latest/](https://copr.fedorainfracloud.org/coprs/openscapmaint/openscap-latest/)

# Downstream Packages
Multiple Linux distributions package ComplianceAsCode content natively. These packages generally provide the most stable experience, and are often supported by your Linux vendor.

Some distributions still package ComplianceAsCode by its previous name, *SCAP Security Guide*. As a result packages are often named ``scap-security-guide``.

## Fedora, Red Hat Enterprise Linux, and CentOS

``
$ sudo yum install scap-security-guide
``

## Debian and Ubuntu
For Debian guides:

``$ sudo apt install ssg-debian``

For Debian-based Distributions, such as Ubuntu:

``$ sudo apt install ssg-debderived``

Non-Debian operating system content, eg to evaluate a RHEL container on a Debian host:
``$ sudo install ssg-nondebian``

Non-Debian application content, such as FireFox and JBoss:
``$ sudo install ssg-application``