# 1. Client installation and DDS instance setup

As we just mentioned, you use the DDS by interacting with command line application, which we call **client**, or **CLI**. This is simply a computer program, which everyone nowadays calls an app, that needs to be installed on you computer.

## A. Client installation

The instructions for installation are available in our documentation, [accessible here.](https://scilifelabdatacentre.github.io/dds_cli/#install-the-command-line-interface-cli-dds-cli)

They differ slightly depending on your operating system, so follow the section you need (MacOS, Windows or Linux). Once installed, verify it by running:

~~~
    dds --version
~~~

![enter image description here](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-version.svg)

# B. Configure the client to use the Test instance of DDS

For today's hands on session you will be using the Test instance of DDS, instead of the Production one. In order to do this, you need to tell the client to use the correct URL.

By default, the client uses the Production instance with the URL: 

> `https://delivery.scilifelab.se`

You can see that URL in the output of any command you run.
 
 ![](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-help-2.svg)
To set the CLI to point to the Test instance you can run the following command in the terminal / command prompt / PowerShell (depending on your OS, see below).

 ~~~
 # Linux / MacOS
export  DDS_CLI_ENV="test-instance"

# Windows Command Prompt
set  DDS_CLI_ENV=test-instance

# Windows PowerShell
$env:DDS_CLI_ENV  =  'test-instance'
 ~~~

###### Subsection tasks
 - [ ] TASK: Run one of the above commands, depending on the OS you are working on.
 - [ ] TASK: Use the help DDS command again and verify that the output contains
 `https://testing.delivery.scilifelab.se/` 
and **not** 
`https://delivery.scilifelab.se/`.