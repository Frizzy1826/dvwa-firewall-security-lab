Project Setup
Apache Installation

Apache was installed on the Ubuntu Server to host DVWA.

sudo apt update
sudo apt install apache2

Apache service status was verified using:

sudo systemctl status apache2
DVWA Installation

DVWA (Damn Vulnerable Web Application) was deployed on the Ubuntu Server.

DVWA was intentionally configured with low security settings to demonstrate common web application vulnerabilities in a safe environment.

Firewall Configuration

UFW (Uncomplicated Firewall) was used to control access to the web application.

Current firewall status:

sudo ufw status

Block HTTP traffic:

sudo ufw deny 80

Block HTTPS traffic:

sudo ufw deny 443
Attack Demonstration
SQL Injection

The SQL Injection vulnerability was tested using DVWA's SQL Injection module.

Example payload:

' OR '1'='1
What Happens?

The application fails to properly validate user input.

Instead of treating the input as data, the application treats it as part of the SQL query.

As a result, database records can be exposed without proper authorization.

Impact
Unauthorized data access
Information disclosure
Potential authentication bypass
Database compromise
Network Testing

Network accessibility was verified before and after firewall enforcement.

Curl Testing
Before Firewall Rules
curl http://TARGET_IP

Result:

HTML page returned successfully

This confirmed that the web application was reachable.

After Firewall Rules
curl --max-time 5 http://TARGET_IP

Result:

Connection timed out

This confirmed that HTTP traffic was blocked.

Nmap Scanning
Before Firewall Rules
nmap TARGET_IP

Result:

80/tcp open
443/tcp open

The service was externally reachable.

After Firewall Rules
nmap TARGET_IP

Result:

80/tcp filtered
443/tcp filtered

The firewall successfully restricted access.
