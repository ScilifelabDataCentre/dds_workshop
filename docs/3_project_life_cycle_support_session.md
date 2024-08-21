# Project life cycle and support session

As we have seen, projects start their life as **In Progress** and end it as **Archived** or **Deleted**, going throuh **Available** and **Expired**

## **In Progress** -> **Available** and back

When created, a project will have status **In Progress**, which means that data can be uploaded and downloaded by Unit staff, but not downloaded by a Researcher. You need to change the status to **Available** in order for Reasearcher users to be able to download. The basic command for changing/checking the project status is `dds project status`:

~~~
$ dds project status
...
 Usage: dds project status [OPTIONS] COMMAND [ARGS]...

 Manage project statuses.
 Display or change the status of a project.
 Displaying the project status is available for all user roles. Changing the project status is
 limited to Unit Admins and Personnel.

╭─ Options ────────────────────────────────────────────────────────────────────────────────────────╮
│ --help      Show this message and exit.                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Commands ───────────────────────────────────────────────────────────────────────────────────────╮
│ archive     Change the project status to 'Archived'.                                             │
│ busy        [Super Admins only] Returns the number of busy projects.                             │
│ delete      Delete an unreleased project (change project status to 'Deleted').                   │
│ display     Display the status of a specific project.                                            │
│ extend      Extend a project deadline by an specified number of days.                            │
│ release     Change project status to 'Available'.                                                │
│ retract     Change the project status to 'In Progress'.                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
~~~

This is the list of actions that can be performed with it.

The sub command `release` changes the state of a project to **Available**:

~~~
dds project status release --project "<Project ID>"
~~~

- [ ] TASK: Explore the `dds project status` command sub commands and their options by running them without specifiyng a partular project.
- [ ] TASK: Release the project after making sure all the data was uploaded, remember to specify the correct project ID.
- [ ] TASK: Check the current project status and the status history.
- [ ] Optional: If you have another email address, use your Unit Admin / Personnel account to invite that email as a researcher. Once you have registered the "researcher" account, authenticate using the researcher account credentials and use the dds data get command as described above to download the data.

If the data in a project needs to be updated, you need to change the status back to **In Progress** unig the sub command `retract`.

- [ ] TASK: Try to upload data to your project when it still has status **Available** and observe the error message.
- [ ] TASK: Use the `dds project status retract` command to change back its status and make a new upload.
- [ ] Optional: If you did the previous optional task, try to download data again intill the project is still **In Progress**.

## **Deleted**

A project can be deleted in cases of incorrect project information or errors, and as result all the data from cloud as well as all the metadata from database get deleted irreversibly. This action is only possible for projects in **In Progress** that have not been previously released. The command for deleting a projects in `dds project delete`

- [ ] TASK: Try to delete your project when it is in **In Progress** and **Available** and note the error messages.
- [ ] TASK: Create a new project, upload some data in it and try to delete it without ever releasing it.
