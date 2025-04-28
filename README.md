# Fawry-Internship-Tasks
## Q1 : Custom Command ( mygrep.sh )
### Reflective Section
#### 1- how your script handles arguments and options?
My script manually checks each argument: it sets flags for -n and -v, 
handles combined options like -vn, then treats the next two arguments 
as the search string and filename and prints lines based on the selected options.




#### 2-If you were to support regex or -i/-c/-l options, how would your structure change?
 I would change the script to use getopts for cleaner option parsing. 
 I would also rely more on grep directly for matching, 
 counting, or listing files, instead of manually reading and processing each line.


#### 3-What part of the script was hardest to implement and why?
The hardest part was handling combined options like -vn correctly while 
still identifying the search string and filename in the right order, 
especially without using getopts.

#### Bonus Features
- Added support for `--help` flag to print usage instructions .
- Improved command-line option parsing using `getopts` for cleaner and more efficient handling of `-n` and `-v` options .

#### Screenshots
- See folder `task 1/`.

## Q2 - Internal Service Unreachable ( Troubleshooting internal.example.com )
1. Verified DNS with dig (local and 8.8.8.8)
2. Diagnosed service with curl and telnet
3. Listed possible causes
4. Applied fixes for DNS, firewall, services
5. Bonus: Used /etc/hosts and systemd-resolved

### Screenshots
- See folder `screenshots/`.




### 1. DNS Verification
- Used dig to check DNS resolution locally and via 8.8.8.8.
- Observed that local DNS failed to resolve, while Google DNS also did not find it.
- Conclusion: Likely an internal DNS or network misconfiguration.
### 2. Service Reachability
- Used curl and telnet to check port 80 and 443 connectivity .
- Found that telnet could not connect (connection refused) .
- Used netstat to check if web server is listening → Web service was NOT listening on external interfaces .

### 3. Possible Causes
```
DNS	-> Incorrect /etc/resolv.conf, DNS server down, internal-only domain
Network	-> Firewall blocking ports, wrong routes
Service	-> Web server down, misconfigured binding to 127.0.0.1

```

### 4. Solutions Applied
```
Problem	                        Confirmation	                Fix
DNS wrong server	       cat /etc/resolv.conf	  Updated to correct DNS IP
Service not listening	        ss -tuln	      Updated server config and restarted web service
Firewall blocking        	sudo ufw              status	Allowed ports 80/443

```
