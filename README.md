*# Project 7 - WordPress Pentesting
Name: Minh Son
Time spent: 10 hours spent in total

> **Objective**: Find, analyze, recreate, and document three vulnerabilities affecting an old version of WordPress (4.2)  

## Pentesting Report

1.  User enumeration through IDOR
* Summary: Using IDOR of site’s URL to identify different user account
* Vulnerability types: User Enumeration
* Tested in version: 4.2
* Fixed in version: N/A
* [Documentation of Attack](https://hackerone.com/reports/335427)

GIF walkthrough

![Alt Text](https://github.com/mhson281/Csuvets/blob/master/User_Enumeration.gif)
  

_Steps to recreate:_ 
* Nov 13, 2019 at 9:10 PM:  Go to the URL http://wpdistillery.vm/wp-login.php
* Nov 13, 2019 at 9:10 PM: Edit the URL with ?author= <id number>
* Nov 13, 2019 at 9:11 PM As different  id number is entered you can see that different users are being referenced in browser and you can see their full name.  This can be further exploit to determine their password.


2. Directory Traversal
	* Summary: Manipulate URL to access site’s js and css repository
		* Vulnerability types: Exposure through directory listing
		* Tested in version:  4.2
		* Fixed in version: Unknown
		* [CWE  548: Documentation of attack](https://www.cvedetails.com/cwe-details/548/Information-Leak-Through-Directory-Listing.html) 
		* GIF Walkthrough: 

![Alt Text](https://github.com/mhson281/Csuvets/blob/master/DirTraversal.gif)

_Steps to recreate:_ 
* Nov 15, 2019 at 8:53 PM: Navigate to http://wpdistillery.vm/wp-admin/css or http://wpdistillery.vm/wp-admin/js
* Nov 15, 2019 at 8:53 PM: Search for files that contains sensitive or exploitable information



3. Cross Site Scripting
	* [ ] Summary: XSS vulnerability that allows the injection of html code
		* Vulnerability types: XSS
		* Tested in version: 4.2
		* Fixed in version: 4.4.1
		* [Documented Here](https://nvd.nist.gov/vuln/detail/CVE-2016-1564)
  [ ] GIF Walkthrough: 
 
![Alt Text](https://github.com/mhson281/Csuvets/blob/master/XSS.gif)


  _Steps to recreate:_ 
* Nov 16, 2019 at 10:34 AM:Navigate to a post on a site and reply with a comment 
* Nov 16, 2019 at 10:35 AM:  Post XSS script 1 listed in the asset portion of the report.  User will get a (1) notification every time the page load.  This vulnerability can be further exploited for more impact.
  
    
## Assets
1. XSS Script:
 http://wpdistillery.vm/"<svg onload=alert(1)>"


## Resources

- [ ] [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [ ] [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

- [ ] Some of the XSS attack that I found did not work in WordPress.  I have tried to reinstall Wordpress multiple time and double checked that it is version 4.2.  However, multiple documented XSS attacks failed to execute.

## License

    Copyright 2019 Minh Son

    Licensed under the Apache License, Version 2.0 (the “License”);
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an “AS IS” BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
