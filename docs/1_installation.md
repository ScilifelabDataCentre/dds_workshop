# 1. Client installation and DDS instance setup

As we just mentioned, you use the DDS by interacting with command line application, which we call **client**, or **CLI**. This is simply a computer program, which everyone nowadays calls an app, that needs to be installed on you computer.

## A. Client installation

The instructions for installation are available in our documentation, [accessible here.](https://scilifelabdatacentre.github.io/dds_cli/#install-the-command-line-interface-cli-dds-cli)

They differ slightly depending on your operating system - MacOS, Windows or Linux. Once installed, the client version can be verified by running:

~~~
    dds --version
~~~

![enter image description here](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-version.svg)

###### Subsection tasks
 - [ ] TASK: Follow the isntructions for your operating system and install the DDS client.
 - [ ] TASK: verify the installation and check the version.

# B. How to use the DDS client

To run the client application, you need to type `dds` in your terminal (normally a terminal emulator app on your computer). The `dds` (main) command has different subcommands, options, and arguments for different kinds of actions.
~~~
    dds [OPTIONS] COMMAND [ARGS]...
~~~

For example, `--version` from the command in the previous section is an option which tells the `dds` command that you only want to check the version of the application.

You can see a complete list of subcommands and options if you run just `dds`:
 ![](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-help-2.svg)

Most subcommands have a set of subcommands on their own.

When you need help with any subcommand as you work through the tasks, use the `--help` flag/option to access helpful documentation directly in the terminal. For instance, running `dds project --help` will display detailed information about that specific command. This information matches what is available on the official documentation site at [scilifelabdatacentre.github.io/dds_cli](https://scilifelabdatacentre.github.io/dds_cli/), making it a convenient way to get quick access to guidance throughout the workshop.

# C. Configure the client to use the Test instance of DDS

For today's hands on sessions you will be using the **Test** instance of DDS, instead of the **Production** one. In order to do this, you need to tell the client to use the correct URL.

By default, the client uses the **Production** instance with the URL:

> `https://delivery.scilifelab.se`

and the URL for the **Test** istance is:

> `https://testing.delivery.scilifelab.se`

You can see that URL in the output of any command you run (including just the main `dds` command).

To set the CLI to point to the **Test** instance you can run the following command in the terminal / command prompt / PowerShell (depending on your OS, see below).

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
 - [ ] TASK: Use the DDS command and verify that the output contains `https://testing.delivery.scilifelab.se/` and **not** `https://delivery.scilifelab.se/`.
 - [ ] TASK: Try several of the available subcommands with the `--help` option to explore the functionality of the DDS client.