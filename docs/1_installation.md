# 1. Installation

The instructions for installation are available in our documentation, [accessible here.](https://scilifelabdatacentre.github.io/dds_cli/#install-the-command-line-interface-cli-dds-cli)

They differ slightly between Mac or Windows. So, follow the section you need. Once installed, verify it by running:

~~~
    dds --version
~~~

![enter image description here](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-version.svg)
## Point to testing

When you run any command, you can notice that, on top of the output, there is a URL, which by default is 

> `https://delivery.scilifelab.se`
 
 ![](https://scilifelabdatacentre.github.io/dds_cli/_images/dds-help-2.svg)
To set the CLI to point to the test instance you can run the following command in the terminal / command prompt / PowerShell (depending on your OS, see below).

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