# Configuration

Once you have a project, service account and gmin_credentials JSON file (see [Getting Started](getting_started.md)), you are ready to complete the gmin configuration.

gmin gets its configuration information from either a configuration file (.gmin.yaml) or operating system environment variables. If both a configuration file and environment variables exist, the environment variables override the configuration file settings.

The `gmin init` and `gmin set config` commands are used to create and update the gmin configuration file.

## init command
In order to create a gmin configuration file, the `gmin init` command is provided. When this command is invoked, you will be prompted to provide configuration information that will be used to create the configuration file. The prompts are as follows:

1. Please enter an administrator email address (q to quit):

This is the email address of the admin user that gmin will impersonate to perform tasks. Therefore, you should enter the email address of an administrator for your Google Workspace domain who has sufficient rights to perform the tasks that you will be requesting via gmin. The address of a super admin is a good choice because they are allowed to perform all admin tasks for a domain.

2. Please enter a full config file path (q to quit)
(Press 'Enter' for default value):

This is the full path to the directory/folder where the .gmin.yaml file will be created. The default is the current user's home directory. If you do enter an alternative path then you will have to enter that path, along with the configuration file name, using the --config flag every time you run a gmin command, for example:

`gmin ls user --config /my/config/path/.gmin.yaml`

3. Please enter a full credentials file path (q to quit)
(Press 'Enter' for default value):

This is the full path to the directory/folder where the gmin_credentials JSON file is located. The default is the current user's home directory.

4. Please enter customer ID (q to quit)
(Press 'Enter' for default value):

This is your Google Workspace customer ID. If you don't know what it is, then you can just press 'Enter' and the default value of 'my_customer' will be used.

5. Please enter a full log file path (q to quit)
(Press 'Enter' for default value):

This is the full path to the directory/folder where log files will be created. The default is the current user's home directory.

6. Please enter a log rotation count (q to quit)
(Press 'Enter' for default value)

This is the maximum number of log files that will be kept. When the maximum number of files is reached, the next log file replaces the oldest.
Default value is 7.

7. Please enter a log rotation time (q to quit)
(Press 'Enter' for default value)

This is the time (in seconds) after which a new log file will be created. Default value is 86400 which is 24 hours.

If you see the message - **init completed successfully** - then you have completed the configuration file setup.

You can test by performing a simple command like `gmin ls users`. If user data is displayed, your setup is good to go.

## set config command

The `gmin set config` command allows you to set configuration file variables once you have a configuration file. It has the following flags:

--admin (-a)<br />
administrator email address

--credential-path (-p)<br />
service account credential file path

--customer-id (-c)<br />
customer id for domain

--log-path (-l)<br />
log file path

--log-rotation-count (-r)<br />
log rotation count

--log-rotation-time (-t)<br />
log rotation time

You can use any or all of these flags in one call, for example:

`gmin set config -a admin@myorg.com -p /my/credential/path -c ynso65ln`

## show config command

The `gmin show config` command will display any gmin environment variables that are set, as well as contents of a configuration file if one exists.

## set credentials command

The `gmin set credentials` command will display a dialogue that allows you to choose a different credentials file to use with gmin. The command displays a list of files (excluding the current gmin_credentials file) contained in the directory/folder that is set in the configuration credential path.

When you choose a file, a copy of it replaces the current gmin_credentials file. This, in conjunction with the `set config` command, allows you to switch between Google Workspace domains if you need to administer more than one.

## Environment Variables

If you don't want to use a configuration file and need or want to user environment variables instead, then you can. The following environment variables can be used to provide the same information that a configuration file provides:

* GMIN_ADMINISTRATOR
* GMIN_CREDENTIALPATH
* GMIN_CUSTOMERID
* GMIN_LOGPATH
* GMIN_LOGROTATIONCOUNT
* GMIN_LOGROTATIONTIME

Set them as required and test by running a simple gmin command. N.B. Environment variables take precedence over configuration file entries.