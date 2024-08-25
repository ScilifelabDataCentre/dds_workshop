# 1. Installation

The instructions for installation are available in our documentation, [accessible here.](https://scilifelabdatacentre.github.io/dds_cli/#install-the-command-line-interface-cli-dds-cli)

They differ slightly depending on your operating system, so follow the section you need (MacOS, Windows or Linux). Once installed, verify it by running:

~~~
    dds --version
~~~

![enter image description here](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-version.svg)

## Using the Test instance of DDS

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


Run the help or version command again and verify that the output contains
 `https://testing.delivery.scilifelab.se/` 
and **not** 
`https://delivery.scilifelab.se/`