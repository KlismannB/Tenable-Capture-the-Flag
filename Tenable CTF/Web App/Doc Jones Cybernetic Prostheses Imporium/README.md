# Doc Jones Cybernetic Prostheses Imporium

> Klismann Barros | February 20, 2021

--------------------------

IP: `167.71.246.232`

# Scanning

`
nmap -sC -sV -Pn -A 167.71.246.232
`

## Nmap Output

	Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
	Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-20 13:10 EST
	Nmap scan report for 167.71.246.232
	Host is up (0.11s latency).
	Not shown: 984 closed ports
	PORT      STATE    SERVICE        VERSION
	22/tcp    open     ssh            OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
	| ssh-hostkey: 
	|   3072 4f:6f:2f:d8:e9:87:ea:1d:57:aa:c7:cd:07:2e:bb:26 (RSA)
	|   256 bb:b7:e6:09:dd:b8:97:0b:4f:ff:08:44:52:b4:1b:4b (ECDSA)
	|_  256 ec:5f:97:52:63:99:73:86:b1:92:66:88:f9:4a:86:08 (ED25519)
	25/tcp    filtered smtp
	70/tcp    filtered gopher
	80/tcp    open     http           Apache httpd 2.4.41 ((Ubuntu))
	| http-robots.txt: 1 disallowed entry 
	|_/admin/
	|_http-server-header: Apache/2.4.41 (Ubuntu)
	|_http-title: Doc Jones Cybernetic Prostheses Imporium
	84/tcp    filtered ctf
	135/tcp   filtered msrpc
	139/tcp   filtered netbios-ssn
	443/tcp   open     ssl/http       Apache httpd 2.4.41 ((Ubuntu))
	| http-robots.txt: 1 disallowed entry 
	|_/admin/
	|_http-server-header: Apache/2.4.41 (Ubuntu)
	|_http-title: Doc Jones Cybernetic Prostheses Imporium
	| ssl-cert: Subject: commonName=flag{selfsignedcert}/organizationName=Doc Jones/stateOrProvinceName=Florida/countryName=US
	| Not valid before: 2021-01-11T22:05:19
	|_Not valid after:  2022-01-11T22:05:19
	| tls-alpn: 
	|_  http/1.1
	445/tcp   filtered microsoft-ds
	593/tcp   filtered http-rpc-epmap
	2323/tcp  filtered 3d-nfsd
	3128/tcp  filtered squid-http
	8080/tcp  open     http           nginx 1.18.0 (Ubuntu)
	|_http-open-proxy: Proxy might be redirecting requests
	| http-robots.txt: 1 disallowed entry 
	|_/admin/
	|_http-server-header: nginx/1.18.0 (Ubuntu)
	|_http-title: Doc Jones Cybernetic Prostheses Imporium
	9898/tcp  filtered monkeycom
	12345/tcp filtered netbus
	31337/tcp filtered Elite
	Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

	Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
	Nmap done: 1 IP address (1 host up) scanned in 34.73 seconds

### Analising the output

	We can see many ports with the STATE 'open', so we can enumerate them:
		22 - SSH - Secure Shell
		80 - HTTP - Hypertext Transfer Protocol
		443 - HTTPS - Hypertext Transfer Protocol Secure
		8080 - Alternative port for HTTP

###### If you pay attention on the 443 port, the ssl-cert (Secure Sockets Layer Certificate) commonName, shows us one of the Flags, you can submit that flag at: Certificate of Authenticity (25 pts).


	The 8080 port has some disallowed entry at the robots.txt file, so we have are going to see this file.

#### Sneaking the /robots.txt

`
curl http://167.71.246.232/robots.txt
`

##### curl output

	User-agent: *
	Disallow: /admin/
	\# flag{mr_roboto}

###### Wohoa! We got another flag, let's submit at: Stay Away Creepy Crawlers (25 pts).

## Looking the website, to see if we can get anything

`
curl http://167.71.246.232/
`

### Analising the website

```HTML
	<html>
	<head>
	<style>
	p{
	        font-size: 20px;
	        color: white;
	}
	h3{
	        color: white;
	}
	b
	{
	        color: white;
	}
	</style>

	<title>Doc Jones Cybernetic Prostheses Imporium</title>
	<body bgcolor='black'>
	        <img src='/images/doc_jones.png'>
	        <h3>Welcome!</h3>
	        <p>Here at Doc Jones Cybernetic Prostheses Imporium, we carry only preem (not second hand - literally) cybernetic prosthesis.  We carry military grade (if you have the right <strike>amount of eddies</strike> credentials), civilian, and industrial augmentations.  If you can't find it, just ask!</p>
	        <p>Side effects of improper installation can include flatline, permanent paralysis, sizeable explosions which could cause collatoral damage, and cyberpsychosis.  But don't worry, because we maintain a gonk free list of Doc Jones certified ripper docs on our virtual portal.<p> 

	        <ul>
	        <b>Menu:</b>
	        <li><a href='certified_rippers.php'>Certified Ripper Docs</a></li>
	        <li><a href='rabbit_hole.php'>Rabbit Hole</a></li>
	        </ul>
	</body>
	
	<!-- source flag : flag{best_implants_ever} -->

	</html>
```

###### And we got another flag, we can submit that at: Source of All Evil (25 pts)

