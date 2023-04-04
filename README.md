# Advanced use of WPScan (WordPress Security Scanner) 
### RedTeam


## Table of Contents 
#### (Basics)
- [Install WPScan](#install-wpscan)
- [Run a basic scan](#run-a-basic-scan)
- [Use options and flags](#use-options-and-flags)
- [WPScan options](#wpscan-options)

#### (Advanced)
- [Use WPScan with other tools](#use-wpscan-with-other-tools)
- [NMAP](#use-wpscan-with-nmap)
- [Nikto](#use-wpscan-with-nikto)
- [Intrusion-Detection-Systemen (IDS)](#use-wpscan-with-intrusion-detection-systemen)
- [OWASP ZAP](#use-wpscan-with-owasp-zap)
- 
#### Misk
- [Warning](#warning)
- [Contributing](#contributing)
- [Credits](#credits)

## About WpScan

WPScan is a free and open source WordPress security scanner that can be used to identify potential vulnerabilities and security issues in WordPress installations. Here's a brief overview of how to use WPScan and some advanced examples. WPScan orginal repositories https://github.com/wpscanteam/wpscan

## Install WPScan
WPScan can be installed on Linux and macOS systems using the command line. You can download the latest version of WPScan from the official GitHub repository:

```shell
$ git clone https://github.com/wpscanteam/wpscan.git
```
### Run a basic scan.
To run a basic scan with WPScan, use the following command:

```shell
$ wpscan --url http://example.com
```
This will scan the WordPress installation at http://example.com and display a summary of the scan results, including the version of WordPress installed, the plugins and themes in use, and any potential vulnerabilities or security issues.

## Use options and flags
WPScan has many options and flags that can be used to customize the scan and improve its accuracy. Here are some examples:
```shell
-e or --enumerate: 
```
This option can be used to enumerate the plugins and themes installed in the target WordPress site. For example:

```shell
$ wpscan --url http://example.com -e vp
```
This will enumerate the installed plugins and themes and display a summary of the results.
```shell
-f or --force: 
```

This option can be used to force a scan of the target WordPress site, even if it has already been scanned before. For example:

```shell
$ wpscan --url http://example.com -f
```
This will force a new scan of the WordPress site, even if it has been scanned before.
```shell
-p or --passwords:
```
This option can be used to test a list of common passwords against the WordPress site's login page. For example:
```shell
$ wpscan --url http://example.com -p password-file.txt
```
This will test the passwords listed in password-file.txt against the WordPress site's login page.

## WPScan options
These options allow you to customize and fine-tune the behavior of WPScan to meet your specific needs and requirements, whether you're performing a basic scan or a more advanced security assessment.

```shell

Usage: wpscan [options]
        --url URL                          The WordPress URL/domain to scan.
        --disable-accept-header           Disable the Accept HTTP header.
        --disable-referer                 Disable the Referer HTTP header.
        --wp-content-dir DIR               WPScan can detect the content directory (ie wp-content) from the homepage but if the website has a custom directory, use this option.
        --wp-plugins-dir DIR               The plugins directory (default: wp-content/plugins).
        --wp-themes-dir DIR                The themes directory (default: wp-content/themes).
        --random-user-agent               Use a random user-agent.
    -v, --verbose                          Verbose output.
        --version                          Display the WPScan version.
    -h, --help                             Display this help message.

Plugin Detection:
        --enumerate[=OPTS]                 List plugins.
                                           Options :
                                             vp  |  Only vulnerable plugins.
                                             ap  |  Only active plugins.
                                             i   |  Only an information about the plugins.
                                             vt  |  Only vulnerable plugins and their version.
                                             at  |  Only active plugins and their version.
        --exclude-content-based REGEXP     Used with the enumeration option (plugins, themes, usernames). Will exclude all entries based on the regexp.
        --detection-mode MODE              Default, Aggressive and Passive modes. Default = mixed.

Theme Detection:
        --enumerate[=OPTS]                 List themes.
                                           Options :
                                             vt  |  Only vulnerable themes.
                                             at  |  Only active themes.

User Enumeration:
        --enumerate[=OPTS]                 List users.
                                           Options :
                                             u   |  Identify the usernames of the authors (and uids) of posts and list them.
                                             m   |  Identify the username of the user connected (if any).
        --exclude-content-based REGEXP     Used with the enumeration option (plugins, themes, usernames). Will exclude all entries based on the regexp.

Password Brute Forcing:
        --wordlist WORDLIST                Path to the wordlist.
        --username USERNAME                Only brute force the supplied username.
        --usernames USERNAMES              A list of usernames to enumerate and brute force.
        --threads THREADS                  The number of threads to use when multi-threading requests.
        --throttle DELAY                    Milliseconds to wait before sending each request. This option is only available in conjunction with the --threads option.

Performance:
        --request-timeout SECONDS          Maximum time in seconds to wait for a response from the web server. The default is 30 seconds.
        --connect-timeout SECONDS          Maximum time in seconds to wait while trying to connect to the web server. The default is 30 seconds.
        --max-threads THREADS              The maximum number of threads to use when multi-threading requests. The default is 50.

Output:
        --output FILE                      Output results to a file.
        --format FORMAT                    Output results in the format specified.
                                           Available formats: cli-no-color, cli, json, xml, yml.

Miscellaneous:
        --update                           Update WPScan.
        --follow-redirection               Follow redirections.
        --batch                            Never ask for user input, use the default behaviour.
        --proxy PROXY                      Supply a proxy in the format host:port.
        --tor                              Use TOR anonymity network.
        --cache-ttl TIME                    Time to keep cached data in seconds. Default is 1800 (30 minutes).
```


## Use WPScan with other tools
WPScan can be used with other tools and plugins to improve its accuracy and effectiveness. For example, you can use WPScan with the WPScan WordPress plugin to perform deeper scans and analysis of the target WordPress site. Additionally, you can use WPScan with other security tools such as Nmap and Nikto to perform more comprehensive security scans.

Note that WPScan is a powerful tool that can be used to identify potential security issues in WordPress installations. However, it's important to use WPScan and other security tools responsibly and ethically, and to follow best practices for securing WordPress sites, such as keeping WordPress and its plugins and themes up-to-date, using strong passwords, and restricting access to sensitive files and directories.

### Use WPScan with NMAP
example of how to use WPScan with Nmap to perform a more comprehensive security scan of a WordPress site:

#### Install and configure Nmap and WPScan on your system
You can download and install the latest version of Nmap from the official website. Similarly, you can download and install WPScan from the official GitHub repository.

Perform an Nmap scan of the target WordPress site.
To perform an Nmap scan of the target WordPress site, use the following command:

```shell
$ nmap -sV --script=http-wordpress-enum <target-ip>
 ```
This will perform a service and version detection scan (-sV) of the target IP address, and run the http-wordpress-enum script to enumerate the installed WordPress plugins and themes.

Use WPScan to perform a more detailed scan of the target WordPress site.
To use WPScan to perform a more detailed scan of the target WordPress site, use the following command:

```shell

$ wpscan --url http://example.com --enumerate vp --plugins-detection mixed --plugins-version-detection mixed
```
This will perform a more detailed scan of the target WordPress site, including enumerating the installed plugins (--enumerate vp), using mixed detection modes for plugin detection and version detection (--plugins-detection mixed --plugins-version-detection mixed), and display a summary of the scan results.

By combining the results of the Nmap and WPScan scans, you can gain a more comprehensive understanding of the security posture of the target WordPress site, including potential vulnerabilities and security issues. Note that these tools should be used responsibly and ethically, and with the permission of the site owner or administrator.
#### Advanced Example:
First, identify open ports and running services on the target web server using Nmap.
```shell
nmap -p- -sV target_website.com
```
This command performs a port scan (-p-) and a service scan (-sV) on target_website.com. This helps you identify open ports and running services that could potentially be vulnerable.

Next, run WPScan to look for known vulnerabilities and misconfigurations in the WordPress system. Example:
```shell
wpscan --url target_website.com
```
You can also use the --enumerate option to get more detailed information about plugins, themes, and users.
```shell
wpscan --url target_website.com --enumerate p,t,u
```
Use the results from the Nmap and WPScan scans to conduct further investigations and tests targeting the identified vulnerabilities.

### Use WpScan with Nikto
Nikto is an open-source web server scanner that checks for potential vulnerabilities, insecure files, outdated server software, and other security issues. It can be a valuable tool for identifying misconfigurations and potential weaknesses in web server setups.

#### Using WPScan and Nikto together

Combining WPScan and Nikto can provide a more comprehensive assessment of a website's security. Follow these steps:

Run WPScan to search for known vulnerabilities and misconfigurations in the WordPress system:
```shell
wpscan --url target_website.com
```
You can also use the --enumerate option to gather more detailed information about plugins, themes, and users. Example:

```shell
wpscan --url target_website.com --enumerate p,t,u
```
Next, use Nikto to perform a comprehensive web server scan to identify potential vulnerabilities and security issues:
```shell
nikto -h target_website.com
```
Here are some additional Nikto options you might find helpful:
```shell
-ssl: To force SSL connections.
-p <port>: To specify a port number to scan.
-output <filename>: To save the scan results to a file.
```

Analyze the results from both WPScan and Nikto to identify potential security issues and vulnerabilities that need to be addressed. This can help you perform a more comprehensive security assessment of the target website.
Remember that using these tools together can provide a more holistic view of a website's security posture and help identify vulnerabilities that may not be detected by one tool alone.

### Use WpScan with Intrusion-Detection-Systemen (IDS)

Intrusion Detection Systems (IDS) are essential tools for monitoring and analyzing network traffic to detect potential security threats. Combining WPScan with an IDS can help you identify and respond to attacks targeting your WordPress website more effectively. Here's how to use WPScan with an IDS:

Set up an IDS like Snort or Suricata on your network or server to monitor traffic and detect suspicious activity. Configure the IDS according to your specific requirements and ensure that it's actively monitoring your network traffic.

Run WPScan to scan your WordPress website for vulnerabilities and misconfigurations:

```shell
wpscan --url target_website.com
```
Use additional WPScan options like --enumerate to gather more detailed information about plugins, themes, and users:

```shell
wpscan --url target_website.com --enumerate p,t,u
```
Monitor the IDS logs and alerts while running WPScan. The IDS may detect unusual or malicious activity during the scanning process, such as repeated login attempts or vulnerability exploitation.

Analyze the IDS logs in conjunction with the WPScan results to identify potential security issues, attacks, or intrusion attempts. This will help you determine whether your WordPress website is being targeted and assess the effectiveness of your security measures.

Adjust your IDS rules and settings as needed to improve detection accuracy and reduce false positives. This may involve tweaking rules to better identify WordPress-specific threats or creating custom rules to detect attacks targeting known vulnerabilities identified by WPScan.

By using WPScan in conjunction with an IDS, you can gain valuable insights into your website's security posture and take appropriate steps to protect it from potential threats. This approach can help you proactively defend your WordPress website and stay ahead of emerging security risks.

### Use WpScan with OWASP ZAP 




# Credits
Copyright Volkan Sah Kücükbudak



