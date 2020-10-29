# Getting Started

## Installing gmin
gmin is intended to be used by Google Workspace admins who are authorised to perform administration tasks. The gmin code lives on [GitHub](https://github.com/plusworx/gmin) and prebuilt executable files are available for Linux, Mac and Windows. Download the executable suitable for your operating system from the [releases page](https://github.com/plusworx/gmin/releases).

In order to use gmin, a bit of set up is required before it can be put to work:

Steps 1 and 2 are completed in the [Google Developer Console](https://console.developers.google.com/).

1. gmin needs a Google Cloud Platform (GCP) Project with the required API(s) enabled. The APIs used are:
* Admin SDK
* Groups Settings API
* Google Sheets API
2. A service account has to be created in the project, that has a JSON key credential file generated for it and has Google Workspace domain-wide delegation enabled.
3. The service account needs to be added to the list of API clients authorised for domain-wide delegation in Google Workspace, along with the required scopes to perform the requested actions. Set up is as follows:
* Go to your Google Workspace admin console
* Click the "Security" icon (or use the search bar)
* Click "App access control"
* Click "MANAGE DOMAIN-WIDE DELEGATION"
* Click "Add new"
* In the "Client ID" field enter the service account's "Client ID" - this can be found in the Google Developer Console under "IAM & Admin" -> "Service Accounts", then "View Client ID" for the newly created service account. It is a ~21 character numerical string.
* In the next field, "OAuth Scopes (comma-delimited)", enter as many of the scopes below as you need and then click "Authorise".

**Please note**: readonly scopes are needed for get,list and batch functions where a Google Sheet is used for data input. The other more permissive scopes are needed for all other functions. Enter all of the scopes if you want full functionality.

<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.chromeos</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.chromeos.readonly</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.mobile</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.mobile.action</div><br />
<div style="display: inline">https://www.googleapis.com/auth/admin.directory.device.mobile.readonly</div><br />
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
<div style="display: inline">https://www.googleapis.com/auth/apps.groups.settings</div><br />
<div style="display: inline">https://www.googleapis.com/auth/drive.readonly</div><br />

4. Copy/move the gmin binary to an appropriate directory/folder and rename the JSON key file, downloaded earlier, to 'gmin_credentials'. Place in a directory/folder suitable for your environment.
5. Run the command `gmin init` and enter the required information to create a gmin configuration file. See the [configuration page](configuration.md) for more details.

Alternatively, you can provide the required configuration information with environment variables. See the [configuration page](configuration.md) for details.

**Please note**: If both a config file and environment variables exist then the environment variables take precedence.

If you want to see what your configuration looks like run the command `gmin show config` and if you need to set configuration file attributes once your config file has been created, use the `gmin set config` command.

6. To see the version number of your gmin binary, run the command `gmin -v` or `gmin --version`.
7. Test that gmin is working correctly by running a simple command such as `gmin list users` or `gmin get user a.user@mydomain.org`. If you see output representing the information requested then you are all set.
8. To get help from gmin itself, enter `gmin -h` or `gmin --help` and go from there.

If you already use [GAM](https://github.com/jay0lee/GAM) then you will already have a service account and JSON credentials file. In this case you could use the same service account by copying the GAM credentials.json, rename the copy to gmin_credentials and place it in the folder/directory that you set for the credentials path when running `gmin init`.

## Usage examples

**Create a new user**

`gmin create user new.user@mydomain.com --first-name New --last-name User --password MyStrongPassword`

with short flag names the above command would look like this -

`gmin crt user new.user@mydomain.com -f New -l User -p MyStrongPassword`

You can set any user attribute via the attributes (-a or --attributes) flag by providing a JSON string.

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

**Create and update commands**

Where an attribute flag (-a or --attributes) is provided for create or update commands, the value can be any valid JSON string that provides attribute values. Please note that if you are setting empty or false values you will either need to use the --force flag with the field names separated by '~', or include a 'forceSendFields' element in your JSON string, otherwise those fields will be ignored.

## Query Flag

Some commands have a query flag (-q or --query) where you can specify query clauses to filter the returned results by. For instance, you might want to retrieve a list of users that have certain attributes -

`gmin list users -q isadmin=true`

This command will return a list of users that have super admin privileges. You could limit the amount of output by specifying the attributes that you want to see for each user, like this -

`gmin list users -q isadmin=true -a primaryemail`

This command will only return the primary email address for each user that satisfies the query.

Similarly to the attributes flag above, query clauses are separated by the tilde (~) character and quotation marks may need to be used. This command returns a list of users whose last name is Smith and has an address in London -

`gmin list users -q lastname=Smith~addressLocality=London`