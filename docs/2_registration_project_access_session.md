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

 # Invite other Unit Staff

When you are the first Unit Admin invited to a new unit, one of the first things to do will be to invite another Unit Admin. Otherwise the system will not allow you to create any projects and will see the following error message if you try to:

~~~
ERROR    Failed to create project: Your unit does not have enough Unit Admins. At least two Unit Admins are required for a project to be created.
~~~
To invite other unit staff, Unit Admins or Unit Personnel (Remember the diagram with the permissions showed in the presentation), you use the `dds user add` command like this:

~~~
dds user add [Email address] --role "Unit Admin"
~~~
or 
~~~
dds user add [Email address] --role "Unit Personnel"
~~~

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

> When an upload is interrupted, you can resume it later on. The system will detect which files are already on the cloud and only ulpload the remaining ones. In order to replace them you must specify the `--overwrite` flag.


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

> NOTE: As of today, DDS can have performance issues and upload failures when uploading many small files. We are working
> on fixing it, but in the meantime, we recommend that you archive (with ZIP or RAR, no compression required) deliveries
> when the delivered data consists of hundreds or thousands of small files.

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

> Currently DDS does not support to resume downloads, if your download is interrupted you will need to restart it.

1. In order for researchers to get access to the data, you need to [change the status](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-access) to `Available`. If a researcher tries to download data and the project is stil in progress they will get an error.

~~~
dds project status release --project "<Project ID>"
~~~

![Message shown after project release](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-project-status-release.svg)
##

After releasing the project, any curent researcher associated with the project will recieve a notification by email.

2. To [invite researchers](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-access-grant) that will download the data to the project:

~~~
dds project access grant --project "<Project ID>" --email "<email>"
~~~

or

~~~
dds user add [Email address] --role "Researcher" --project "<Project ID>"
~~~

> There is no practical difference between these two commands for this use case. However, as mentioned above, it is 
> possible to automatically invite researchers when creating a project. `dds project create (...) --researcher [Email address]`



##
3. To [download](https://scilifelabdatacentre.github.io/dds_cli/data/#dds-data-get) the full project contents
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


##
4. Download specific contents

There could be some scenarios where you don't need to get the full project contents. For that, there are two options you can use. Above, the `--source` option was explained and used. You can also use the `--source-path-file` one.

Here are examples on how to use them based on our sample data:

~~~
dds data get 
    --source "data/example_directory_1/sub_directory_1/"
    --source "data/example_directory_2/sub_directory_2/example_file_3.txt" 
    --source "data/example_directory_2/example_file_5.txt" 
    --project "<Project ID>"
~~~

You can pack all this different source routes with the spf option:

~~~
dds data get 
    --source-path-file spf.txt
    --project "<Project ID>"
~~~

Where spf.txt is the path to an **existing** file which has the following format:

>cat spf.txt
~~~
data/example_directory_1/sub_directory_1/
data/example_directory_2/sub_directory_2/example_file_3.txt
data/example_directory_2/example_file_5.txt
~~~


