# Getting Started

## Installing gmin
gmin is intended to be used by G Suite admins who are authorised to perform administration tasks. The gmin code lives on [GitHub](https://github.com/plusworx/gmin) and prebuilt executable files are available for Linux, Mac and Windows. Download the executable suitable for your operating system from the releases page.

In order to use gmin, a bit of set up before it can be put to work:

Steps 1 and 2 are completed in the [Google Developer Console](https://console.developers.google.com/).

1. gmin needs a Google Cloud Platform (GCP) Project with the required API(s) enabled. At present gmin only uses the Admin SDK APIs.
2. A service account has to be created in the project, that has a JSON key credential file generated for it and has G Suite domain-wide delegation enabled.
3. The service account needs to be added to the list of API clients authorised for domain-wide delegation in G Suite, along with the required scopes to perform the requested actions. Set up is as follows:
* Go to your G Suite admin console
* Click the "Security" icon (or use the search bar)
* Click "App access control"
* Click "MANAGE DOMAIN-WIDE DELEGATION"
* Click "Add new"
* In the "Client ID" field enter the service account's "Client ID" - this can be found in the Google Developer Console under "IAM & Admin" -> "Service Accounts", then "View Client ID" for the newly created service account. It is a ~21 character numerical string.
* In the next field, "OAuth Scopes (comma-delimited)", enter as many of the scopes below as you need and then click "Authorise".

**Please note**: readonly scopes are needed for get and list functions. The other more permissive scopes are needed for
create, delete, update and undelete functions. Enter all of the scopes if you want full functionality.

<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.chromeos</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.chromeos.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.group</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.group.member</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.group.member.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.group.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.orgunit</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.orgunit.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.user</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.user.alias</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.user.alias.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.user.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.userschema</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.userschema.readonly</div><br />

4. Copy/move the gmin binary to a convenient directory/folder and rename the JSON key file, downloaded earlier, to 'gmin_credentials'. Place in a directory/folder suitable for your environment.
5. Run the command `gmin init` and enter the required information:

* Email address of the admin whose privileges will be used (mandatory).
* Path where config file, .gmin.yaml, will be written. Default is current user's home directory. If you choose a different installation path to the default for the config file then that path will need to be given with each gmin command by using the --config flag.
* Path where service account credentials json file is stored. File must be named 'gmin_credentials'. Default is current user's home directory.
* Customer ID. Default is 'my_customer'.

Alternatively, you can provide the required information with environment variables:

* GMIN_ADMINISTRATOR
* GMIN_CREDENTIALPATH
* GMIN_CUSTOMERID

**Please note**: If both a config file and environment variables exist then the environment variables take precedence.

If you want to see what your configuration looks like run the command `gmin show config` and if you need to set configuration file attributes once your config file has been created, use the `gmin set config` command.

6. To see the version number of your gmin binary, run the command `gmin -v` or `gmin --version`.
7. Test that gmin is working correctly by running a simple command such as `gmin list users` or `gmin get user a.user@mydomain.org`. If you see output representing the information requested then you are all set.
8. To get help from gmin itself, enter `gmin -h` or `gmin --help` and go from there.

If you already use [GAM](https://github.com/jay0lee/GAM) then you will already have a service account and JSON credentials file. In this case you could use the same service account by copying the GAM credentials.json, rename the copy to gmin_credentials and place it in the folder/directory that you set for the credentials path when running `gmin init`.

## Usage examples

**Create a new user**

`gmin create user new.user@mydomain.com --firstname New --lastname User --password MyStrongPassword`

with abbreviations the command would look like this -

`gmin crt user new.user@mydomain.com -f New -l User -p MyStrongPassword`

The user object has a lot of attributes and there are only flags for the most commonly-used ones. However, you can set any user attribute via the attributes (-a or --attributes) flag by providing a JSON string.

Therefore the user above could be created by using the following command -

`gmin create user new.user@domain.com -a '{"name":{"givenName":"New","familyName":"User"},"password":"MyStrongPassword"}'`

When creating objects, values provided by the attributes flag are overriden by attributes provided by other flags. For example -

`gmin crt user d.williams@mycompany.org -f Danny -l Williams -p SuperSecretPwd -a '{"name":{"givenName":"Douglas"}}'`

would result in a user whose first name is Danny not Douglas.

**Get a user**

`gmin get user new.user@mydomain.com`

This command results in all user information being returned. If I only want their addresses then I would say -

`gmin get user new.user@mydomain.com -a addresses`

If I only want a particular part of the address, because address is made up of other attributes, I could say something like -

`gmin get user new.user@mydomain.com -a "addresses(formatted)"`

**List users**

`gmin list users`

This command returns all user information about all users. If I want to restrict the amount of information returned then I can specify some attributes -

`gmin list users -a primaryemail~name~addresses`

If I want to filter the results still further I can provide a query with or without attributes -

`gmin list users -q orgunitpath=/Sales`

**Delete a user**

`gmin delete user new.user@mydomain.com`

There are no warnings issued by the delete command so use it carefully.

**Undelete a user**

`gmin undelete user new.user@mydomain.com`

This allows you to restore a user that has been deleted.

## Attributes Flag

**Get and list commands**

These commands have an attribute flag (-a or --attributes) where you can specify particular object attributes that you want to see in the results. If the attribute is not present (including false or empty) then it will not be displayed.

https://developers.google.com/admin-sdk/directory/v1/reference is a useful resource for looking up valid attribute names and values.

**Create and update commands**

Where an attribute flag (-a or --attributes) is provided for create or update commands, the value can be any valid JSON string that provides attribute values. Please note that if you are providing empty or false values you will need to use the --force flag with the field names separated by '~' otherwise those fields will be ignored.

## Query Flag

Some commands have a query flag (-q or --query) where you can specify query clauses to filter the returned results by. For instance, you might want to retrieve a list of users that have certain attributes -

`gmin list users -q isadmin=true`

This command will return a list of users that have super admin privileges. You could limit the amount of output by specifying the attributes that you want to see for each user, like this -

`gmin list users -q isadmin=true -a primaryemail`

This command will only return the primary email address for each user that satisfies the query.

Similarly to the attributes flag above, query clauses are separated by the tilde (~) character and quotation marks may need to be used. This command returns a list of users whose last name is Smith and has an address in London -

`gmin list users -q lastname=Smith~addressLocality=London`

https://developers.google.com/admin-sdk/directory/v1/get-start/getting-started is a useful resource for looking up query parameters. There are 'Search for' links for different objects like Users and Groups.
