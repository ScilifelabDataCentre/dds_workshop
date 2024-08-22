# 2. Getting started as a Unit User

## A. Account registration and accessing the system


You should have received a registration link from 

> services-noreply@scilifelab.se

This link is to register a new account, in the testing instance and in a custom unit for this workshop. Open the link and create a new account.

Once that is done. Run
~~~
dds auth login
~~~

Examples on how to use it are available in the [documentation.](https://scilifelabdatacentre.github.io/dds_cli/examples/#authentication-dds-auth)

![Screenshot of the login steps](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-auth-login.svg)

After completing authentication, dds-cli will automatically save an authentication token file (.dds_cli_token) by default in your home directory. You have the possibility to specify the location and the filename of the token file, but we will explore this functionality in the end of this session

 - [ ] TASK: Find the email and create an account and login using your information. Note that the password will not be shown while you are typing it. Make sure your password is a strong one.
 - [ ] TASK: Display information about your just created account using the command `dds user info`. It is important to remember the username you've just chosen. We recommend usage of password management tool for handling your username and password. 
 - [ ] TASK: Try to find the token file in you home directory and check its content.

#### Inviting other Unit Staff

When you are the first Unit Admin invited to a new unit, one of the first things to do will be to invite another Unit Admin. Otherwise the system will not allow you to create any projects and will return the following error message if you try to:

~~~
ERROR    Failed to create project: Your unit does not have enough Unit Admins. At least two Unit Admins are required for a project to be created.
~~~

To invite other unit staff, Unit Admins or Unit Personnel (remember the diagram with the permissions showed in the presentation), you use the `dds user add` command like this:

~~~
dds user add [Email address] --role "Unit Admin"
~~~
or 
~~~
dds user add [Email address] --role "Unit Personnel"
~~~

You will not need to do this today because you are all invited as Unit Admin.

## B. Project creation, data upload, and invitation of Researchers

#### Create a project

The command for creating project has the following general syntax:

~~~
dds project create --title "<Project Title>" --description "<Project Description>" --principal-investigator "<Email to PI>"
~~~

> The email specified in the option `--principal-investigator` does not receive any emails or creates any account; it’s only for information purposes at this time.

When the project is created, you should get an output similar to the one below. Record the **Project ID**, as you will need it to access the project later on.

![Screenshot of a successful project creation](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-project-create.svg)

> You can always retrieve the the **Project ID** using the command `dds ls` and then setting meaningful `--title` and `--description` will prove useful for you.

<<<<<<< HEAD:docs/2_registration_project_access_session.md
 - [ ] TASK: Run the create project command, remember to change the fields of **title**, **description** and **pi**

=======
>>>>>>> main:docs/2_getting_started_session.md
> There are other flags that can be passed down, like `--owner` to add a user as a Project Owner (researcher with elevated privileges), or `--researcher`, to automatically invite researcher users to the project. The list and description can be found in the [documentation](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-create) linked here.

 - [ ] TASK: Run the create project command, remember to change the values for `--title`, `--description` and `--pi`
 - [ ] TASK: Use the command `dds ls` or `dds project ls` to confirm is shown in the output. Observe the information shown in the table.

#### Upload data

When created, the project will have status "In progress", which means that data can be uploaded, but not downloaded.

The general upload command is [`dds data put`.](https://scilifelabdatacentre.github.io/dds_cli/data/#dds-data-put)
~~~
dds data put --project "<Project ID>" --source "<File or directory to upload>"
~~~

> There are a number of other optional flags, which can be found in the [documentation](https://scilifelabdatacentre.github.io/dds_cli/data/#dds-data-put) link here.

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

On Windows, you can use the `dir` command or manually explore the structure through the File Explorer.


 - [ ] TASK: Upload the files in the data folder. Remember to change the **project ID** and the **source** from the command above

> When an upload is interrupted, you can resume it later on. The system will detect which files are already on the cloud and only ulpload the remaining ones. In order to replace them you must specify the `--overwrite` flag.

If you have forgotten the project ID, you can list all active projects to which you have access with the `ls` command, [see documentation](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-ls) here.

~~~
dds project ls
~~~

> NOTE: As of today, DDS can have performance issues and upload failures when uploading many small files. We are working
> on fixing it, but in the meantime, we recommend that you archive (with ZIP or RAR) deliveries when the delivered data consists of hundreds or thousands of small files.
> On Mac/Linux this can be achieved with:
> `tar -czf data.zip data/` for compression. 
> `tar -xzf data.zip` for decompression.  

#### List contents

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

#### Release project and download data

> Currently DDS does not support to resume downloads, if your download is interrupted you will need to restart it.

1. In order for researchers to get access to the data, you need to [change the status](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-access) to `Available`. If a researcher tries to download data and the project is still in progress they will get an error.

~~~
dds project status release --project "<Project ID>"
~~~

![Message shown after project release](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-project-status-release.svg)
##

After releasing the project, any current researcher associated with the project will receive a notification by email.

##
3. To [download](https://scilifelabdatacentre.github.io/dds_cli/data/#dds-data-get) the full project contents:
~~~
dds data get --get-all --project "<Project ID>" 
~~~


##
4. Download specific contents

There could be some scenarios where you don't need to get the full project contents. For that, there are two options you can use. You can use the `--source` option to specify which file or directory you want to download within the project. If you want to download multiple individual files or directories, specify the `--source` option multiple times.

~~~
dds data get --source "<1st file or directory>" --source "<2nd file or directory>" [... etc] --project "<Project ID>"
~~~

You can also use the `--source-path-file` option, which allows you to put all the different files and/or directories in a text file and pass this file
to the uploading command.

Here are examples on how to use these two options based on our sample data:

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

Where spf.txt is the path to a file you have created with the following format:

~~~
data/example_directory_1/sub_directory_1/
data/example_directory_2/sub_directory_2/example_file_3.txt
data/example_directory_2/example_file_5.txt
~~~

 - [ ] TASK: Release the project after making sure all the data was uploaded, remember to specify the correct project ID
 - [ ] TASK: Download the project contents, and verify that they are the correct. You can download data with your unit admin account.

#### Researchers

In real scenarios, the data you've uploaded will be downloaded by researchers. To [invite researchers](https://scilifelabdatacentre.github.io/dds_cli/project/#dds-project-access-grant), you can use the command:

~~~
dds user add [Email address] --role "Researcher" --project "<Project ID>"
~~~



> It is also possible to automatically invite researchers when creating a project. `dds project create (...) --researcher [Email address]`


 - [ ] Optional: If you have another email address, use your Unit Admin / Personnel account to invite that email as a researcher. Once you have registered the "researcher" account, authenticate using the researcher account credentials and use the dds data get command as described above to download the data.

> Another command to invite researchers is `dds project access grant --project "<Project ID>" --email "<email>" `

