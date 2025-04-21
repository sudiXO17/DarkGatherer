# DarkGatherer
Welcome to the ultimate reference list of enumeration, scanning, password cracking, and dark web info gathering commands! This repository serves as a personal cheatsheet and toolkit for your red teaming and pentesting needs.

---

## 📌 Table of Contents

- [🔍 Enumeration Commands](#-enumeration-commands)
- [🏯️ Scanning Tools](#-scanning-tools)
- [🔓 Password & Hash Cracking](#-password--hash-cracking)
- [🌐 Surface & Dark Web OSINT](#-surface--dark-web-osint)

---

## 🔍 Enumeration Commands

```bash
# Fingerprinting & Information Gathering
wafw00f http://10.10.109.34
dnsenum example.com
dig example.com any
whois example.com
whatweb http://example.com
wappalyzer http://example.com
theHarvester -d example.com -b all

# Subdomain & Directory Discovery
subfinder -d vulnweb.com -o subfinder_results.txt
gobuster dir -u http://10.10.109.34 -w directory-list-2.3-medium.txt

# Fuzzing with FFUF
ffuf -u https://FUZZ.example.com -w subdomains.txt -mc 200 -o subdomains.txt
ffuf -u https://example.com/FUZZ -w directories.txt -mc 200,301 -o directories.txt
ffuf -u https://example.com/FUZZ -w big.txt -recursion -recursion-depth 3 -o recursive_dirs.txt
ffuf -u https://example.com/FUZZ -w common.txt -e .php,.html,.js,.txt -o files.txt
ffuf -u https://example.com -w subdomains.txt -H "Host: FUZZ.example.com" -o waf_bypass.txt
ffuf -u "https://example.com/index.php?FUZZ=test" -w parameters.txt -mc 200 -o parameters.txt
ffuf -u "https://example.com/FUZZ" -w common.txt -e .js -o js_files.txt
```

---

## 🏯️ Scanning Tools

```bash
# SSL & HTTPS Scanning
sslscan example.com
testssl example.com

# Vulnerability Scanning
nuclei -u http://vulnweb.com/ -t vulnerabilities/ -severity medium,high,critical -c 50 -rl 100 -stats -o nuclei-results.txt
nikto -h target.com -p 80,443,8080,8443 -C all -Tuning x 6 -output nikto_scan.txt

# CMS & Platform-Specific
wpscan --url https://elementor.com/ --random-user-agent --ignore-main-redirect --max-threads 50 --force

# SQLi & Command Injection
sqlmap -u http://www.site.com/vuln.php?id=1 --dbs --random-agent --level=5 --risk=3 --batch
commix -u "http://www.site.com/vuln.php?id=1" --random-agent --level=3 technique= C, T, E, F --batch --all

# Nmap with Vuln Scripts
nmap -sV --script=vulscan/vulscan.nse www.example.com
nmap -p 80,443,8080,8443 --script=http-vuln*,http-wordpress-enum,http-joomla-brute,http-sql-injection,http-xssed,http-brute,ssl-enum-ciphers,ssl-cert,ssl-heartbleed,http-title,http-server-header,http-fileupload-exploiter,http-open-redirect,http-waf-detect,http-waf-fingerprint -T4 -A -v target.com

# HTTP Stress Testing
python3 goldeneye.py http://testphp.vulnweb.com -w 10 -s 200 -m get
```

---

## 🔓 Password & Hash Cracking

```bash
# John the Ripper
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt ntlm_hashes.txt

# Hashcat
hashcat -m 1400 -a 0 hash.txt rockyou.txt
hashcat -m 13600 -a 0 zip.hash rockyou.txt

# Hash Identification
hashid hash.txt

# Brute Forcing - Hydra
hydra -L users.txt -P passwords.txt 192.168.1.100 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=Invalid login"
hydra -L users.txt -P passwords.txt <protocol>://<target> [options]

# Brute Forcing - Medusa
medusa -h 192.168.1.100 -U users.txt -P passwords.txt -M ssh

# Cracking ZIP files
ffmpeg -i adcd.mp4       # Check video format
file secret.zip          # Inspect file
zip2john secret.zip > zip.hash
john --wordlist=rockyou.txt zip.hash
```

---

## 🌐 Surface & Dark Web OSINT

```bash
# Onion & Dark Web Queries
onionsearch "testphp.vulnweb.com" --proxy socks5://127.0.0.1:9050 --output onion_results.txt --limit 50

# Email Intelligence
h8mail -t emails.txt -o results.csv
holehe test@example.com --proxy socks5://127.0.0.1:9050

# Web Crawler
photon -u "https://www.vulnhub.com/" --wayback --output photon_results

# Recon Framework
spiderfoot -s target.com -t DOMAIN_NAME,USERNAME,EMAIL -o csv -q
```

---

## 📁 Contributing

Feel free to submit pull requests to add more commands, tools, or improvements! Let's make this the go-to repository for red teamers, CTF players, and OSINT hunters.

---

## 📜 License

This repository is open-source and available under the [MIT License](LICENSE).

---

## 🙌 Support & Acknowledgments

If you found this repo useful, give it a ⭐ and consider contributing back! Huge thanks to the developers behind the amazing tools used here.

