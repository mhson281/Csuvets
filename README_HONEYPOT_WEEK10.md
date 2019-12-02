# *Weeks 10 & 11 Project: Honeypot*
Name: Minh Son

Time spent: **10** hours spent in total
* Milestone 0: To the Cloud!

* Milestone 1: Create MHN Admin VM

*  Milestone 2: Install the MHN Admin Application

*  Milestone 3: Create a MHN Honeypot VM

*  Milestone 4: Install the Honeypot Application

*  Milestone 5: Attack!

Set Up:
- [ ] For this project, I signed up for a free GCP account with a free 1 year subscription and $300 in credit.

- [ ] Create a MHN admin VM with the following specs:
*Ubuntu 18.04 Minimal
*HTTP traffic allowed (port 80)
*TCP ports 3000 and 10000 need to be open to allow incoming traffic for geolocation and honeypot sensor data.
- [ ] Set up firewall to allow port 80, 3000, and 1000:

gcloud compute firewall-rules list

gcloud compute firewall-rules create http \
    —allow tcp:80 \
    —description**=**”Allow HTTP from Anywhere” \
    —direction ingress \
    —target-tags**=**”mhn-admin”

gcloud compute firewall-rules create honeymap \
    —allow tcp:3000 \
    —description**=**”Allow HoneyMap Feature from Anywhere” \
    —direction ingress \
    —target-tags**=**”mhn-admin”

gcloud compute firewall-rules create hpfeeds \
    —allow tcp:10000 \
    —description**=**”Allow HPFeeds from Anywhere” \
    —direction ingress \
    —target-tags**=**”mhn-admin”

- [ ] Install MHN application on the newly created mhn-admin

*Update the vm and install python dependency:
sudo apt update
sudo apt install git python-magic -y

*Install mhn-admin application to manage all honeypots:
$ sudo git clone https://github.com/threatstream/mhn.git
  $ cd mhn/
  $ sudo ./install.sh

*After installation, a number of services should be running. To check:
   $ sudo supervisorctl status 

- [ ] Create the actual honeypot:
**Demo on creating a MHN Honeypot**

![Alt Text](https://github.com/mhson281/Csuvets/blob/master/Create_Honeypot.gif)



**Which Honeypot(s) you deployed**
    1. dionaea with HTTP
    2. Snort


- [ ] Install the honeypot application on honeypot VM:

* Login to your MHN server web app.
* Click the “Deploy” link in the upper left hand corner.
* Select a type of honeypot from the drop down menu (e.g. “Ubuntu 12.04 Dionaea”).
* Copy the deployment command.
* Login to a honeypot server and run this command as root.

- [ ] Attack the honeypot via Kali Linux and record data:
*Demo:
![Alt Text](https://github.com/mhson281/Csuvets/blob/master/Kali_Scan_Nmap.gif)

*Check the mhn-admin console for incoming attacks:
![Alt Text](https://github.com/mhson281/Csuvets/blob/master/mhn_console.gif)


# # Attacks in the last 24 hours:
# 10,050

[10,050](http://35.239.20.93/ui/attacks/?hours_ago=24)
# TOP 5 Attacker IPs:
**1.** *  * [37.216.253.134 (3,827 attacks)](http://35.239.20.93/ui/attacks/?source_ip=37.216.253.134) 
**2.** *  * [201.76.0.132 (2,833 attacks)](http://35.239.20.93/ui/attacks/?source_ip=201.76.0.132) 
**3.** *  * [27.45.234.74 (1,779 attacks)](http://35.239.20.93/ui/attacks/?source_ip=27.45.234.74) 
**4.** *  * [196.202.39.32 (1,417 attacks)](http://35.239.20.93/ui/attacks/?source_ip=196.202.39.32) 
**5.** *  * [188.19.191.108 (28 attacks)](http://35.239.20.93/ui/attacks/?source_ip=188.19.191.108) 
# TOP 5 Attacked ports:
**1.**  [1433 (9,858 times)](http://35.239.20.93/ui/attacks/?destination_port=1433) 
**2.**  [23 (76 times)](http://35.239.20.93/ui/attacks/?destination_port=23) 
**3.**  [8088 (30 times)](http://35.239.20.93/ui/attacks/?destination_port=8088) 
**4.**  [445 (20 times)](http://35.239.20.93/ui/attacks/?destination_port=445) 
**5.**  [4243 (6 times)](http://35.239.20.93/ui/attacks/?destination_port=4243) 
 


- [ ] Export data to a JSON file 
*First, SSH into the mhn-admin console and run:

mongoexport —db mnemosyne —collection session > session.json

This will direct the collected data into the session.json file
*Second, export the session.json file to local machine:

gcloud compute scp mhn-admin:~_session.json ._session.json

![Alt Text](https://github.com/mhson281/Csuvets/blob/master/session.json)

Issues and Concerns:
* My mhn-admin might not have been installed properly.  Initially, attacks against honeypot-1 (dionaea) were not being captured.  I re-installed the mhn-admin server and it was able to record attacks.  However, the flag of the source country IPs did not show up.  Some additional features did not show up as well.
* Attacks against my honeypot-2(snort) are not being recorded as well.  I think it might have something to do with my mhn-admin not being installed properly.


