 # Steps to Enum WebApp 
 
 > Created by [`Ethical Hitler 🔥`](https://github.com/EthicalHitler)



### 1. DNS Enumeration
First make sure you enumerate DNS records since it may contain a text record which reveals some information.

```bash
$ nslookup -type=any domain
```
- nslookup - command to resolve DNS
- type=any - Returns any type of DNS record
- domain - specify the URL
***
### 2. Subdomain Enumeration

After DNS Enum , we should perform sub domain enum since some sub domain may contain sensitive information or it can lead us to the main domain.

- You can use any tools like DNS recon or any online tools
```bash
$ dnsrecon -d Domain -D Wordlist -t brt
```
***
### 3. SSL Certificates

Whenever a site is provided with SSL cert , a new public record is being created for that SSL in the server. This can be verified using [`Crt.sh`](https://crt.sh/)
Here you can verify the certs and even can find anything useful.
***
### 4. Directory Bruteforcing
Always consider doing a directory bruteforcing in a suspicious URL since it may hide any directories which contains hint or valuable information.
This is used mostly in web based CTF Challenges.
So there are 2 tools that I use to bruteforce.

##### Gobuster
```bash
$ sudo apt-get install gobuster #installation
$ gobuster dir -u url -w wordlist #usage
``` 
- dir - specifies directory bruteforcing method 
##### FFUF
```bash
$ sudo apt-get install ffuf #installation
$ ffuf -w wordlist -t 1 -p 0.1 -H "cookie: admin" -u url/FUZZ -fc 404
``` 
- t - specifies thread count 
- p - specifies delay between each request
- H - used to specify the headers
- fc - used to filter any HTTP requests based on the status codes 
***
### 5. Login Bruteforcing
If there is a login page and if it returns **`Username is invalid`** or **`Password is invalid`** then we have a great chance of guessing the credentials. Usually I use Hydra as my goto tool for creds bruteforce.
##### Hydra
```bash
$ hydra -l <username> -P <password list> <Target hostname> <service module> <post request parameters>[/code]
```
You can use ffuf also.
#### FFUF
```bash
$ ffuf -w wordlist -t 1 -p 0.1 -H "cookie: admin" -X POST -d "username=FUZZ&password=x" -u url -fc 404
```
***


## Download Links

> **Note:** Here I use **Kali Linux** , a debian based  distro hacking so the commands wary for your distro. 

### Tools
- [`DNSRecon`](https://github.com/darkoperator/dnsrecon)
- [`Hydra`](https://github.com/vanhauser-thc/thc-hydra)
- [`FFUF`](https://github.com/ffuf/ffuf)
### Wordlists
- [`Rockyou.txt`](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt)
- [`Seclists`](https://github.com/danielmiessler/SecLists)