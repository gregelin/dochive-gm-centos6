# Status

| Date         | Status |
|--------------|-------------|
| Jan 17, 2014 | Under development  |

For additional status visit [STATUS.md](STATUS.md)

# About

This repo is to create a GitMachines version of Doc Hive on CentOS 6.

Our goals:

- [x] First, a **one-click install of Raleigh Public Record's [Dochive](https://github.com/raleighpublicrecord/dochive/tree/master/dochive)**.
- [ ] Second, **basic scans for security auditing** as part of the install. 
- [ ] Third, **transparent documentation to make multi-machine configuration easier.** 
- [ ] Finally, **a Statedecoded GitMachine - fully accreditation-ready, one-click install of DocHive on a virtual machine**, ready for easy adoption.

** Warning this is a work in progress - Please check branches for activity**

# Versions

## 
| Version | Description |
|---------|-------------|
| v0.1 nice | one-click install of tesseract |

## How can I contribute?
We are learning as we go and do not yet clear asks to make of others. However, you can:
- Follow along, try things, and submit issues
- Fork, hack, and make pull requests (PLEASE keep these small for now and related to our project goals).

## Why this project?
DocHive uses "templates" to extract regions of PDF images and OCR the text from that region of the document. 

Setting up all the software can be involved and take hours. 

At GitMachines we are interested in one-click installs to get accreditation-ready builds in order to encourage adoption.

## Status
### What our one-click build does..

1. Uses CentOS, which is very very close to RedHat Enterprise

### What user needs to do...
1. Clone repo and cd into repo directory
2. Type `vagrant up`
3. Surf web for a few minutes

## Dependencies
  * Latest version of vagrant (vagrantup.com)
  * Latest version Virtualbox (4.2.10 guest additions on our base box)
  * Do not have service running on ports 8080 or 8081 on host computer.

## Instructions

### One-click build and (simple) audit run
```
  # Clone this repo locally to your computer and switch to repo directory.
  git clone git@github.com:GitMachines/dochive-gm-centos6.git
  cd dochive-gm-centos6
  
  # Stop any running virtual machines that might conflict on ports 8080 and 8081.
  # Launch your gitmachine 
  vagrant up
  # Browse the web, b/c this will take a while. 

  # Your statedecoded GitMachines is running on http://localhost:8080
  # Openscap has been installed and a very (very) simple scan is run 

  # Check out your GitMachine!
  open audit/home.html

```

### (Optional) SSH into your gitmachine and run the SCAP test manually
You can run your own audit checks using installed openscap `oscap` from the command line steps.

``` 
  vagrant ssh
  
  # Re-run sample scap script
  /vagrant/resources/scripts/oscap-rhel6.sh

  # Reports are available in audit/reports directory.

  # Want to run your own scan, here is the command format from oscap-rhel6.sh

oscap xccdf eval --profile stig-rhel6-server \
  --results /vagrant/audit/reports/results-stig-rhel6-server.xml \
  --report /vagrant/audit/reports/report-stig-rhel6-server.html \
  --cpe /usr/share/xml/scap/ssg/content/ssg-rhel6-cpe-dictionary.xml \
  /usr/share/xml/scap/ssg/content/ssg-rhel6-xccdf.xml

```

## Why CentOS instead of Ubuntu?
- Bit compatibility with RedHat Enterprise Linux (RHEL) since RHEL is popular with is common/popular among governments and businesses.
- We want cities to adopt Statedecoded and RHEL has government acceptance b/c it is built on SELinux (Security Enhanced Linux) 
- SELinux has elements, like default firewall (/etc/sysconfig/iptables) that Ubuntu does not
- OpenSCAP (Security Content Automation Protocols) and base line control configurations already exist for CentOS but do not yet for Ubuntu (from what we can tell). We need SCAP to produce the scans and audit reports to make Statedecoded accreditation-ready. 

## Why from scratch?
- To learn.
- To deal easier with CentOS's built-in firewall.
- To automate OpenSCAP scanning and reporting.
- To see if we can streamline and further automate the install.
- To rethink how documentation can be managed and even driven from code.
- Because some installations will require the database to be run on a different server from the application and to have other redundancies. We want to understand how to create a path for varying configurations.

## ToDo
See the issues.
