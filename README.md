# Explore Google hacking and enumeration 

# AIM:

To use Google for gathering information and perform enumeration of targets

## STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various Google hacking keywords and enumeration tools as follows:


### Step 3:
Open terminal and try execute some kali linux commands

## Pen Test Tools Categories:  

| Operator    | Description                        | Example Usage           |
| ----------- | ---------------------------------- | ----------------------- |
| `site:`     | Search within a specific domain    | `site:example.com`      |
| `inurl:`    | Search in URL                      | `inurl:admin`           |
| `intitle:`  | Search in page title               | `intitle:"index of"`    |
| `filetype:` | Search by file type                | `filetype:pdf`          |
| `intext:`   | Search inside page text            | `intext:"confidential"` |
| `link:`     | Pages that link to a specific site | `link:example.com`      |
| `cache:`    | View cached version of a site      | `cache:example.com`     |
| `ext:`      | Same as filetype                   | `ext:xls`               |

 ## Architecture 
 ```
+----------------------+
|   Attacker / Hacker  |
|   (Browser & Google) |
+----------+-----------+
           |
           | Google Dork Queries
           v
+---------------------------+
|       Google Search       |
+---------------------------+
           |
           | Indexed Public Content
           v
+---------------------------+
|   Target Websites / Data  |
| - Leaked files            |
| - Open directories        |
| - Sensitive info          |
+---------------------------+

```

# Output:
## SITE:
<img width="1918" height="1077" alt="image" src="https://github.com/user-attachments/assets/68a24221-2478-42f3-839d-de3121de73c8" />


## INURL:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/f0f2da05-0f38-44ba-9ffc-7cb3a029dd02" />


## INTITLE:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/fbd81476-bf1d-45ca-9a4e-f48a4e7e491c" />


## FILETYPE:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/4c9134aa-f01f-4639-826e-aed9b3d3916a" />


## INTEXT:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/33cc2efe-ca39-4ff5-a87a-1a2eb3f86d6e" />


## LINK:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/87ede532-bae4-4166-9629-e02da273e8fe" />


## CACHE:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/966dbf6b-f041-43b1-aebe-6f3b036f5208" />


## EXT:
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/c4306ab6-1b1c-4e53-9b17-54b0503d88c2" />



# DNS Enumeration
<img width="1920" height="1051" alt="kali linux  Powered Off  - Oracle VirtualBox 08-09-2025 21_24_50" src="https://github.com/user-attachments/assets/be14b456-31c4-4f04-b5be-7aff86d76253" />



## DNS Recon
<img width="1920" height="1051" alt="kali linux  Powered Off  - Oracle VirtualBox 08-09-2025 21_27_35" src="https://github.com/user-attachments/assets/f55f16d5-505c-456d-98bd-ad4db258f9c6" />


| Record Type | Meaning                        | Example Output                   |
| ----------- | ------------------------------ | -------------------------------- |
| A           | Host to IPv4 address           | `example.com -> 93.184.216.34`   |
| AAAA        | Host to IPv6 address           | `example.com -> ::1`             |
| MX          | Mail server info               | `mail.example.com`               |
| NS          | Name servers                   | `ns1.example.com`                |
| TXT         | Misc data (SPF, verifications) | `v=spf1 include:_spf.google.com` |
| CNAME       | Canonical names (aliases)      | `www -> example.com`             |

## Common Tools Used (Kali Linux)

| Tool           | Description                                | Usage Example                           |
| -------------- | ------------------------------------------ | --------------------------------------- |
| `nslookup`     | DNS lookup tool (simple queries)           | `nslookup example.com`                  |
| `dig`          | DNS lookup utility (detailed)              | `dig example.com any`                   |
| `host`         | Simple DNS querying tool                   | `host example.com`                      |
| `dnsenum`      | Perl script to enumerate DNS info          | `dnsenum example.com`                   |
| `fierce`       | DNS scanner to locate non-contiguous IPs   | `fierce -dns example.com`               |
| `dnsrecon`     | Powerful DNS enumeration script            | `dnsrecon -d example.com -a`            |
| `theHarvester` | Subdomain enumeration using search engines | `theHarvester -d example.com -b google` |


## OUTPUT:

## Architecture Diagram 
```
+-------------------+        +------------------+       +------------------+
|                   |        |                  |       |                  |
|   Attacker (You)  +------->|   Target Server   +<----->+    DNS Server    |
| Kali Linux / Parrot|       | (Mail / DNS Host) |       |  (Authoritative) |
+---------+---------+        +---------+--------+       +---------+--------+
          |                            ^                          ^
          |                            |                          |
          |                            |                          |
          |           +-----------------------------+            |
          |           |      Information Tools      |            |
          |           |-----------------------------|            |
          |           | smtp-user-enum              |            |
          |           | nmap --script smtp-enum-*   |            |
          |           | dnsenum                     |<-----------+
          |           +-----------------------------+
          |
          v
+-----------------------------+
|   Output/Report             |
|  - Usernames Found          |
|  - MX Records / Zones       |
|  - Subdomains / IPs         |
+-----------------------------+

```

## dnsenum
**Purpose:** A multithreaded Perl script to enumerate information from DNS servers.

**Use case:** Performs DNS zone transfers, brute force subdomains, and gather host IPs.

```
dnsenum example.com
```

## Output:






## smtp-user-enum
**Purpose:** Standalone tool used to enumerate valid users by using the VRFY, EXPN, or RCPT TO commands.

**Use case:** Brute-forces SMTP to find users.

```
smtp-user-enum -M VRFY -U users.txt -t <target-ip>
```
  
 ## Output
  


## nmap –script smtp-enum-users.nse <hostname>

**Purpose:** Uses smtp-enum-users NSE script to enumerate valid users on an SMTP server.

**Use case:** Helps identify email accounts on mail servers.

```
nmap -p 25 --script smtp-enum-users.nse <target-ip>
```
## OUTPUT:



## RESULT:
The Google hacking keywords and enumeration tools were identified and executed successfully
