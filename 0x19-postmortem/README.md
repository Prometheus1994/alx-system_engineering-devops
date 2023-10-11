<div align="center">
  <h1>Postmortem: Web Stack Outage</h1>
</div>

## Issue Summary:
- **Duration:** *October 7, 2023, 10:00 AM - October 7, 2023, 11:50 AM (UTC)*
- **Impact:** Oh, the horror! Our primary web application took a coffee break. Around *80%* of users had to sip extra coffee as they faced slow response times, intermittent errors, and the urge to start a support group for frustrated users.
- **Root Cause:** The servers threw a party and invited everyone - a surge in traffic gave our database servers a headache, causing them to stutter and stall.

## Timeline:
+ **10:00 AM (UTC):** — The issue was detected by several users, who contacted the customer service department.
+ **10:05 AM (UTC):** — The issue was escalated to the System Engineering team, and the SRE.
+ **10:10 AM (UTC):** — They looked at the running processes on the server using ‘ps auxf’ to see if any unwanted child process was running in the background, and keeping the server from responding.
+ **10:30 AM (UTC):** — After seeing the processes looked fine, the team used ‘strace’ on some process ids including the ones of apache2 (the web server hosting the wordpress page).
+ **10:45 AM (UTC):** — strace on one of the apache2 processes was showing an infinite loop of system calls, so they looked at the second apache2 process.
+ **11:00 AM (UTC):** — When using curl on the page’s IP while running strace on that second apache2 process, the team realized strace was displaying a lot of errors. One of them said that the file index.html didn’t exist, but it was a misleading clue because adding that file in the wordpress folders didn’t seem to make it work.
+ **11:15 AM (UTC):** — After reading carefully all the errors returned by strace, the team saw that one of them mentioned that a file didn’t exist: the file that apache2 was trying to access seemed to be terminating in ‘.phpp’, which is not a common extension for a file.
+ **11:30 AM (UTC):** — When looking at the wordpress settings file, /var/www/html/wp-settings.php, line 137 was trying to require that faulty file. From then, the team just removed the extra ‘p’ at the end of the extension.
+ **11:50 AM (UTC):** — The team only had to restart apache2 using ‘service apache2 restart’. The page was back up like normal.

## Root cause and Resolution:
- A typo. They are very Annoying! The WordPress app was encountering a critical error in wp-settings.php when trying to load the file class-wp-locale.phpp. The correct file name, located in the wp-content directory of the application folder, was class-wp-locale.php.
- Patch involved a simple fix on the typo, removing the trailing p.

## Corrective and Preventative Measures:
**To tackle this issue head-on and guard against future surprises, we're taking these steps:**

1. **Comprehensive Testing:**
   - We're enhancing our testing procedures to include a wider range of user interaction scenarios, aiming to catch those rare cases.

2. **Improved Logging and Monitoring:**
   - Our plans include investing in better logging and monitoring to spot unusual user behaviors and system responses in real time.

3. **Code Review and Refactoring:**
   - We'll be delving into our code with a keen eye, identifying and refining areas that may be prone to similar cascading failures.

4. **User Education:**
   - We're working on better educating our users on the most effective platform usage practices to reduce the chances of triggering unusual issues.

5. **Disaster Recovery Drills:**
   - Regular drills are in the pipeline to test our incident response procedures under complex and unexpected scenarios.

6. **Communication and Transparency:**
   - We're committed to improving our communication with users during incidents, providing clear and timely updates on our progress and resolutions.

In conclusion, the recent outage was the result of an extraordinary and intricate set of circumstances. We've acted swiftly to address the issue and are implementing measures to ensure the resilience and stability of Hbtn in the face of the unexpected. We apologize for any inconvenience this incident may have caused and appreciate the patience and understanding of our users during this challenging time.
