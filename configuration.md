# Configuration

Once you have a project, service account and gmin_credentials JSON file (see [Getting Started](getting_started.md)), you are ready to complete the gmin configuration.

gmin gets its configuration information from either a configuration file (.gmin.yaml) or operating system environment variables. If both a configuration file and environment variables exist, the environment variables override the configuration file settings.

The `gmin init` and `gmin set` commands are used to create and update the gmin configuration file.

## init command
In order to create a gmin configuration file, the `gmin init` command is provided. When this command is invoked, you will be prompted to provide configuration information that will be used to create the configuration file. The prompts are as follows:

1. Please enter an administrator email address:

This is the email address of the admin user that gmin will impersonate to perform tasks. Therefore, you should enter the email address of an administrator for your Google Workspace domain who has sufficient rights to perform the tasks that you will be requesting via gmin. The address of a super admin is a good choice because they are allowed to perform all admin tasks for a domain.

2. Please enter a full config file path (Press 'Enter' for default value):

This is the full path to the directory/folder where the .gmin.yaml file will be created. If you press 'Enter' without typing anything, then the configuration file will be created in the current user's home directory. If you enter a path then you will have to enter that path, along with the configuration file name, using the --config flag every time you run a gmin command, for example:

`gmin ls user --config /my/config/path/.gmin.yaml`

3. Please enter a full credentials file path (Press 'Enter' for default value):

This is the full path to the directory/folder where the gmin_credentials JSON file is located. If you press 'Enter' without typing anything, then the path will be the current user's home directory.

4. Please enter customer ID (Press 'Enter' for default value):

This is your Google Workspace customer ID. If you don't know what it is, then you can just press 'Enter' and the default value of 'my_customer' will be used.

If you see the message - **\*\*\*\* gmin: init completed successfully \*\*\*\*** - then you have completed the configuration file setup.

You can test by performing a simple command like `gmin ls users`. If user data is displayed, your setup is good to go.

## set config command

The `gmin set config` command allows you to set configuration file variables. It has the following flags:

--admin (-a)<br />
administrator email address

--credentialpath (-p)<br />
service account credential file path

--customerid string (-c)<br />
customer id for domain

You can use any or all of these flags in one call, for example:

`gmin set config -a admin@myorg.com -p /my/credential/path -c ynso65ln`

## show config command

The `gmin show config` command will display any gmin environment variables that are set, as well as contents of a configuration file if one exists.

## Environment Variables

If you don't want to use a configuration file and need or want to user environment variables instead, then you can. The following environment variables can be used to provide the same information that a configuration file provides:

* GMIN_ADMINISTRATOR
* GMIN_CREDENTIALPATH
* GMIN_CUSTOMERID

Set them as required and test by running a simple gmin command.