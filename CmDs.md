## ☣️ Few Cmds

- `subfinder -d fb.com | httpx -title -ports 80,443,8443`
    - Sub-domains of `fb.com`
    - Httpx to get page title & check ports `80,443,8443` for these sub-domains.
- `subfinder -d fb.com | httpx -title -status-code content-length -silent`
    - Sub-domains of `fb.com`
    - Httpx to return the status codes, titles, content-length for each sub-domain, silently displaying the results. 
- `seq 1 10 | ffuf -u "http://fb.com/cmt?token=FUZZ" -w - `
    - Generates a sequence of numbers from 01 to 10 and uses FFUF to inject them into the URL's token parameter, testing different values.
- `turbosearch -t https://fb.com -w wordlist.txt`
    - Using Turbosearch to search for directories and files on the website using specific wordlists.
- `echo htpp://fb.com | waybackurls | kxxs `
    - `KXSS` & `WAYBACKURLS` - It passes urls to `WaybackUrls` to retrive archived URLs, and then uses `KXSS` to find potential `XSS vulns` in those URLs.

# Few tools for Ethical hacking
## OSINT
[Certina](# "Gather detailed information about your targets from various public sources.")&emsp;&emsp;
[NetScout](# "Gain comprehensive visibility into network traffic and performance for effective OSINT.")

## Web 
[PingRAT](# "Use ICMP payloads to pass command and control traffic through firewalls undetected.")&emsp;&emsp;
[SiteDorks](# "Use advanced search queries to uncover vulnerabilities and gather detailed information on targets.")&emsp;&emsp;
[go-dork](# "Utilize Google Dorking techniques to uncover sensitive information exposed online and perform advanced reconnaissance.")&emsp;&emsp;
[Horus](# "A powerful tool for data gathering with features like location tracking, IP tracing, and file encryption.")&emsp;&emsp;
[FinalRecon](# "Perform detailed reconnaissance on target websites, gathering in-depth information on structure and vulnerabilities.")&emsp;&emsp;
[SmuggleFuzz](# "Discover how to test and exploit HTTP request smuggling vulnerabilities to secure your web applications.")&emsp;&emsp;
[pphack](# "Scan websites for client-side prototype pollution vulnerabilities and understand how to exploit them.")&emsp;&emsp;
[WAF Bypass](# "Test the resilience of your web applications against sophisticated attacks that evade WAF protections.")&emsp;&emsp;
[Upload_Bypass](# "Identify and exploit vulnerabilities in file upload mechanisms to ensure secure web applications.")&emsp;&emsp;
[403jump](# "Bypass HTTP 403 (Forbidden) pages using various techniques to audit web application security.")

## IoT
[Genzai](# "Scan and analyze IoT dashboards for vulnerabilities, focusing on default passwords and software exploits.")

## Android    
[apk2url](# "Extract URLs from Android APK files and gather valuable OSINT on application backend infrastructure.")

## WiFi
[Freeway](# "Conduct Wi-Fi penetration testing to identify and exploit vulnerabilities in wireless networks.")

## Phishing    
[mailMeta](# "Analyze email metadata to uncover phishing attempts and trace email origins.")&emsp;&emsp;
[MalStatWare](# "Quickly analyze malware by extracting static attributes and performing initial file assessments.")&emsp;&emsp;
[dnstwist](# "Detect typosquatting and phishing attempts by generating domain permutations.")

## Red Team
[Troll-A](# "Learn about advanced penetration testing and red teaming with this tool designed for simulating sophisticated attacks.")&emsp;&emsp;
[RustRedOps](# "Access advanced techniques and malware for red team operations, focusing on the Rust programming language.")

## DDoS    
[DDoSlayer](# "Simulate advanced Layer 7 DDoS attacks to stress-test web services and identify vulnerabilities.")