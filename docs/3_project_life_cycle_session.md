# Project life cycle

As we have seen, projects start their life as **In Progress** and end it as **Archived** or **Deleted**, going through **Available** and **Expired**

## Releasing and retracting a project

When created, a project will have status **In Progress**, which means that data can be uploaded and downloaded by Unit staff, but not downloaded by a Researcher. You need to change the status to **Available** in order for Researcher users to be able to download. The basic command for changing/checking the project status is `dds project status`:

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

- [ ] TASK: Explore the `dds project status` command sub commands and their options by running them without specifying a particular project.
- [ ] TASK: Release the project after making sure all the data was uploaded, remember to specify the correct project ID.
- [ ] TASK: Check the current project status and the status history.
- [ ] Task: Use your Researcher account token file to run the `dds data get` command as described above and download the data.

If the data in a project needs to be updated, you need to change the status back to **In Progress** using the sub command `retract`.

- [ ] TASK: Try to upload data to your project when it still has status **Available** and observe the error message.
- [ ] TASK: Use the `dds project status retract` command to change back its status and make a new upload. Observe the error messages when you try to upload the same data and when using the `--overwrite` option.
- [ ] Task: Try to download data again as a Researcher while the project is still **In Progress**.

## *Deleted*

A project can be deleted in cases of incorrect project information or errors, and as a result, all the data from the cloud, as well as all the metadata from the database get deleted irreversibly. This action is only possible for projects in **In Progress** that have not been previously released. The command for deleting a project is `dds project status delete`

- [ ] TASK: Try to delete your project when it is in **In Progress** and **Available** and note the error messages.
- [ ] TASK: Create a new project, upload some data in it and try to delete it without ever releasing it.
- [ ] TASK: Use the project listing command with the option `--show-all` to see the list of projects including the deleted one.

## *Expired*

Projects are **Available** for a certain (chosen by the units) period of time, Days in Available (DiA). After that their status automatically changes to **Expired**. Data cannot be changed in this state, but the project can be re-released up to *two times*. After two re-releases, a project can only be archived.

- [ ] TASK: Check the current project status and the status history. Observe the deadline date for the current status.

## *Archived*

A project has the status **Expired** for a certain number of Days In Expired (DiE), after which the project status is automatically changed to **Archived**. All data is deleted, metadata is retained and this status is irreversible.

Project archiving can be done manually by a Unit account, using the command `dds project status archive`

- [ ] TASK: Create a new project, upload some data to it and then archive it.
- [ ] TASK: Use the project listing command to confirm the project is archived.
- [ ] TASK: Create a new project, upload some data in it and then archive it using the `--abort` option. Observe the output of the command.
