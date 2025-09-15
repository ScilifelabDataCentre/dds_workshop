According to the event, our **preliminary agenda** is: 

09:00-09:30: Coffee
09:30-09:40: Welcome & Practical info
09:40-10:00: Intro to DDS
10:00-10:45: Registration, client installation
10:45-11:00: Coffee
11:00-12:00: Projects
12:00-13:00: Lunch
13:00-13:45: Project life cycle
13:45-14:00: Break
14:00-15:00: Support model, future development, feedback

# 09:30-09:40: Welcome & Practical info

- Who are we
- Agenda
- Breaks
- Other
    - Fire exits? 

# 09:40-10:00: Intro to DDS

- Data Delivery System 
- We built it because 
- Not for long term storage -- Project statuses ties in
- Currently CLI which communicates to API 
- Currently building GUI -- status of this at the end of the day 

# 10:00-10:45: Registration, client installation

- They should have gotten invites to the dev / testing (??) instance
- Guide them through how they register 
- How do they install the CLI? 
    - Options: PyPI or executable
    - If PyPI: create a venv first
    - If executable: make actually executable
- How to log in 

# 11:00-12:00: Projects

- DDS is project centred -- need a project for everything 
- Step by step of delivery flow + hands-on
    1. Create project
    2. List projects
    3. Upload data
    4. List project contents
    5. Give access to user 

# 13:00-13:45: Project life cycle

- Overview of the different statuses? + Imagined lifecycle? 
- When project created: "In Progress"
    - Upload allowed
    - Download allowed for unit users, but not others 
    - No deadline, and there is currently no reminder -- don't forget about it, delete it if you're not using it anymore, otherwise you pay for the storage in that project
- When we want to allow download from users --> release the project: "Available" 
    - Upload **not** allowed
    - Download allowed
    - Deadline depends on unit
- After certain time (deadline) --> "Expired" 
    - Data kept, metadata kept 
    - You can renew access again, "re-release" --> deadline applies again
    - Renewal of access or deadline extension possible twice -- 3 times in available possible 
- No renewed access --> automatic archivation of project: "Archived"
    - Data deleted, metadata kept 
    - Natural end of project life cycle 
    - You can also archive manually 
- Other statuses: "Deleted" and "Aborted"
    - Deleted: Only possible from "In Progress"
    - Aborted: Subcategory of "Archived"
- How to change project status + hands-on  
    - "Now that we have created a project and uploaded data, we want to give someone access to that data." 
    - Extend project deadline
    - Rerelease project ?? (not sure if we can make this testable in a simple way) 

# 14:00-15:00: Support model, future development, feedback

- Support model: 
    - You help your users
    - We help you if you cannot solve the issue yourselves 
    - Take help from documentation 
    - Email us at ... 
- Plan for the future: 
    - GUI 
    - .... 
- GUI demo -- current status 
- Feedback session 
