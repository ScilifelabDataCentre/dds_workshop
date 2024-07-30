# 2. Registration and project access



You should have received a registration link from 

> services-noreply@scilifelab.se

This link is to register a new account, in the testing instance and in a custom unit for this workshop. Open the link and create a new account.

Once that is done. Run
~~~
dds auth login
~~~

Examples on how to use it are available in the [documentation.](https://scilifelabdatacentre.github.io/dds_cli/examples/#authentication-dds-auth)

![Screenshot of the login steps](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-auth-login.svg)

 - [ ] TASK: Find the email and create an account and login using your information. Note that the password will not be shown while you are typing it.

# Create a project

~~~
dds project create --title "<Project Title>" --description "<Project Description>" --principal-investigator "<Email to PI>"
~~~

> The email specified in the option `--principal-investigator` does not receive any emails or creates any account; it’s only for information purposes at this time.

[Docs.](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-create)
When the project is created, you should get an output similar to the one below. Remember the **Project ID**

![Screenshot of a sucessfull project creation](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-project-create.svg)

 - [ ] TASK: Run the create project command, remember to change the files of **title**, **description** and **pi**

> There are other flags that can be passed down, like `--owner` to add a user as a Project Owner (researcher with elevated privileges). Or `--researcher` to automatically invite researcher users to the project. The list and description can be found on the documentation link just above.

# Upload data

By default, the project will be "In progress" (which means that data can be uploaded, but not downloaded).

Check the folder which contains the data, on Mac/Linux, inside this repository.
~~~
ls -R data/
~~~

> example_directory_1     example_directory_2
> 
> data/example_directory_1: sub_directory_1
> 
> data/example_directory_1/sub_directory_1: example_file_1.txt
> 
> data/example_directory_2: example_file_2.txt      example_file_5.txt  
> sub_directory_2
> 
> data/example_directory_2/sub_directory_2: example_file_3.txt     
> example_file_4.txt

On windows, you can use the `dir` command or manually explore the structure through the file explored.


The general upload command is [`dds data put`.](https://scilifelabdatacentre.github.io/dds_cli/data/#dds-data-put)
~~~
dds data put --project "<Project ID>" --source "<File or directory to upload>"
~~~

> There are a number of other optional flags, which cab be found on the documentation link just above.

> NOTE: As of today, DDS can break when there are heavy uploads. We are working on fixing it, but on the meantime, we recommned to ZIP files when the uploads are big (Hundreds of files).


 - [ ] TASK: Upload the files in the data folder. Remember to change the **project ID** and the **source** from the command above

If you have forgotten the project ID, you can list all active projects you have access with: [Docs](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-ls)

~~~
dds project ls
~~~

# List contents

You can interactively list the contents of a project with the [`ls` command:](https://scilifelabdatacentre.github.io/dds_cli/data/#dds-data-ls)
~~~
dds data ls --project "<Project ID>"
~~~

However, you can view all files and directories in a project as a tree structure, using the `--tree` option.

~~~
dds data ls --project "<Project ID>" --tree
~~~

![Screenshot of the files structure in the project](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-data-ls-tree.svg)

 - [ ] TASK: Verify that all the data has being uploaded succesfully.

# Release project and download data


1. In order for researchers to get access to the data, you need to [change the status](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-access) to `Available`.

~~~
dds project status release --project "<Project ID>"
~~~

![enter image description here](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-project-status-release.svg)
##

2. To [invite researchers](dds%20user%20add%20%5BEmail%20address%5D%20--role "&lt;Account role&gt;quot; --project quot;&lt;Project ID&gt;") that will download the data to the project:

~~~
dds project access grant --project "<Project ID>" --email "<email>"
~~~

or

~~~
dds user add [Email address] --role "Researcher" --project "<Project ID>"
~~~

##
3. To download the full project contents
~~~
dds data get --get-all --project "<Project ID>" 
~~~

You can also use the `--source` option to specify which file or directory you want to download within the project. If you want to download multiple individual files or directories, specify the `--source` option multiple times.

~~~
dds data get --source "<1st file or directory>" --source "<2nd file or directory>" [... etc] --project "<Project ID>"
~~~

 - [ ] TASK: Release the project after making sure all the data was uploaded, remember to specify the correct project ID
 - [ ] TASK: Download the project contents, and verify that they are the correct. You can download data with your unit admin account.
 - [ ] Optional: Use another email you may have to invite yourself as a researcher, you don't need to register again.


 # Invite other Unit Staff

You can invite other unit staff, Unit Admins or Unit Personnel. (Remember the diagram with the permissions showed in the presentation)

The command is similar to the one used before

~~~
dds user add [Email address] --role "Unit Admin"
~~~
or 
~~~
dds user add [Email address] --role "Unit Personnel"
~~~
