---
title: "Web Server - Apache2"
date:  2023-04-06T12:00:00+00:00
description: "Install Apache2 to configure Web Server."
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
asciinema: true
tags:
- P-TECH
series:
-
categories:
- 
image: images/2023-thumbs/apache2.webp
---
#### Exercises to complete:
1. Install Apache2
2. Enable and start Apache2
3. Add a port to firewalld
4. Create a simple website
5. Check does the website display correctly using IP address

<script async id="asciicast-575077" src="https://asciinema.org/a/575077.js"></script>

#### Install Apache2

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  To install Apache2 type:
  ```
  # refresh repositories
  sudo zypper ref
  # install Apache2
  sudo zypper -n in apache2
  # enable Apache2 on boot
  sudo systemctl enable apache2
  # start the Apache2
  sudo systemctl start apache2
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  To install apache2 type:
  ```
  # refresh repositories
  sudo apt update
  # install apache2
  sudo apt -y install apache2
  # enable apache2 on boot
  sudo systemctl enable apache2
  # start the apache2
  sudo systemctl start apache2
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  To install apache2 type:
  ```
  sudo yum install httpd -y
  or
  sudo dnf install httpd -y
  # enable apache2 on boot
  sudo systemctl enable httpd
  # start the apache2
  sudo systemctl start httpd
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Allow Apache2 service

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  linux:~ # sudo firewall-cmd --add-service=http --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo ufw allow 'WWW'
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  linux:~ # sudo firewall-cmd --add-service=http --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Create a simple webiste

```
echo 'Linux fundamentals - lab' | sudo tee -a /srv/www/htdocs/index.html
```

#### Check does the website display correctly using IP address

```
curl http://checkip.amazonaws.com
curl http://IP-ADDRESS
```

#### Manage Apache2 logs

If you want to display the real-time request of Apache access logs and monitor the realtime log request, type command:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo tail -f /var/log/apache2/access_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo tail -f /var/log/apache2/access.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo tail -f /etc/httpd/logs/access_log
  sudo tail -f /var/log/httpd/access_log
  ```
  {{< /tab >}}
{{< /tabs >}}

If you want to check your Apache2 error logs, type command:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo tail -f /var/log/apache2/error_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo tail -f /var/log/apache2/error.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo tail -f /etc/httpd/logs/error_log
  sudo tail -f /var/log/httpd/error_log
  ```
  {{< /tab >}}
{{< /tabs >}}

You can limit the number of lines to display from your logs (e.g 100), by using the command -n option.

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo tail -n 100 /var/log/apache2/access_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo tail -n 100 /var/log/apache2/access.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo tail -n 100 /etc/httpd/logs/error_log
  sudo tail -n 100 /var/log/httpd/error_log
  ```
  {{< /tab >}}
{{< /tabs >}}

Note: The logs view starts at the end of the line and is printed to the standard output.

#### Display a Specific Term from Access Logs

Sometimes, you only want to display a specific type of entry in the log.  You can use the grep command to filter your report by certain keywords.

For example, enter the following into a terminal:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo grep GET /var/log/apache2/access_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo grep GET /var/log/apache2/access.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo grep GET /etc/httpd/logs/access_log
  sudo grep GET /var/log/httpd/access_log
  ```
  {{< /tab >}}
{{< /tabs >}}

Like the previous command, this looks at the /var/log/apache2/access.log file to display the contents of the access log. The grep command tells the machine to only display entries with the GET request.

You can substitute other Apache commands as well. For example, if you’re looking to monitor access to .jpg images, you could substitute .jpg for GET. As before, use the actual path to your server’s log file.

#### Interpreting the Access Log in Apache

When you open your access log file for the first time, you may feel overwhelmed.

There’s a lot of information about HTTP requests, and some text editors (and the terminal) will wrap the text to the next line. This can make it confusing to read, but each piece of information is displayed in a specific order.

The conventional method for expressing the format of access log files is:

"%h %l %u %t "%r" %>s %b "%{Referer}i" "%{User-agent}i""

This is a code for the most common things in each line of the log.

Each % sign corresponds to a piece of information in the log:

* %h – The client’s IP address (the source of the access request).
* %l – This next entry may simply be a hyphen — that means no information was retrieved. This is the result of checking identd on the client.
* %u – Client’s userid, if the access request required http authentication.
* %t – Timestamp of the incoming request.
* %r – Request line that was used. This tells you the http method (GET, POST, HEAD, etc.), the path to what was requested, and the http protocol being used.
* %>s – Status code that was returned from the server to the client.
* %b – Size of the resource that was requested.
* "%{Referer}i" – This tells you if the access came from clicking a link on another website, or other ways that the client was referred to your page.
* "%{User-agent}i" – Tells you information about the entity making the request, such as web browser, operating system, website source (in the case of a robot), etc.

Just read across the line in your log file, and each entry can be decoded as above. If there is no information, the log will display a hyphen. If you’re working on a preconfigured server, your log file may have more or less information. You can also create a custom log format by using the custom log module.

For more information about decoding log formats, see this page.

#### How to Use Data in Apache Log Files

Apache log analysis gives you the opportunity to measure the ways that clients interact with your website.

For example, you might look at a timestamp to figure out how many access requests arrive per hour to measure traffic patterns. You could look at the user agent to find out if particular users are logging in to a website to access a database or create content. You could even track failed authentications to monitor various types of cybersecurity attacks against your system.

The apache error log can be used similarly. Often, it’s simply used to see how many 404 errors are being generated. A 404 error happens when a client requests a missing resource, and this can alert you on broken links or other errors within the page. However, it can also be used to find configuration glitches or even warnings about potential server problems.

#### Conclusion

This guide provided methods for extracting data to view Apache access log files.

The access.log file is an excellent resource for measuring the ways that clients are interacting with your server. The error.log file can help you troubleshoot issues with your website.