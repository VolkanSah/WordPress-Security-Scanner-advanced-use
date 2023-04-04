# Advanced use of WPScan (WordPress Security Scanner) - RedTeam
WPScan orginal repositories https://github.com/wpscanteam/wpscan

## Table of Contents (Basics)
- [Install WPScan](#install-wpscan)
- [Run a basic scan](#run-a-basic-scan)
- [Use options and flags](#use-wpscan-options-and-flags)
- [WPScan options](#wpscan-options)

## [Admin Panel](#use-wpscan-with-other-tools)
- [Admin Panel](#the-admin-panel)
- [User Panel](#the-user-panel)
- [Usage](#usage)
- [Credits](#credits)
- [Contributing](#contributing)
- [License](#license)

WPScan is a free and open source WordPress security scanner that can be used to identify potential vulnerabilities and security issues in WordPress installations. Here's a brief overview of how to use WPScan and some advanced examples:

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

## c
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

### Use WpScan with Nikto


### Use WpScan with Intrusion-Detection-Systemen (IDS)

### Use WpScan with OWASP ZAP 







# Credits
Volkan Sah



