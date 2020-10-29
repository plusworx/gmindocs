# Managing Users

This section contains information about the commands that you can use to manage Google Workspace users.

## batch-create users

**Command aliases**:<br />
bcreate, bcrt<br />
user, usrs

**Flags**:<br />
--format (-f) input format (valid values: csv, gsheet, json) json is the default<br />
--input-file (-i) Path to input file or Google Sheet ID<br />
--sheet-range (-s) Google sheet data range in the format 'Sheet1!A1:C10'

**Input data**: CSV file, Google Sheet, JSON file or piped JSON input

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-create users command allows you to create multiple Google Workspace users with one command. It takes input data in any of the formats detailed above and outputs a message for each user that it creates. If an error is encountered, it is logged, displayed to the console if the --silent flag is not used and processing continues to the next record.

CSV files and Google Sheets must contain a header row and the row headings must be valid user attribute names. Both CSV files and Google Sheets do not allow input of nested information, therefore the only valid attributes are as follows:

* changePasswordAtNextLogin [value true or false]
* firstName or givenName [required]
* includeInGlobalAddressList [value true or false]
* ipWhitelisted [value true or false]
* lastName or familyName [required]
* orgUnitPath
* password [required]
* primaryEmail [required]
* recoveryEmail
* recoveryPhone [must start with '+' in E.164 format]
* suspended [value true or false]

These names are case insensitive and can be provided in any order.

JSON data for each user is expected on separate lines like this:

    {"name":{"firstName":"Stan","familyName":"Laurel"},"primaryEmail":"stan.laurel@company.com","password":"SecretPassword",changePasswordAtNextLogin":true}
    {"name":{"givenName":"Oliver","familyName":"Hardy"},"primaryEmail":"oliver.hardy@company.com","password":"SecretPassword","changePasswordAtNextLogin":true}
    {"name":{"givenName":"Harold","familyName":"Lloyd"},"primaryEmail":"harold.lloyd@company.com","password":"SecretPassword","changePasswordAtNextLogin":true}

**Examples**:<br />
`gmin bcrt users -i /path/to/file/inputfile.json`
`gmin bcrt user -i /path/to/file/inputfile.csv --format csv`
`gmin batch-create usrs -i 1zpyC6XzvTdKT5EIUywvqESX3A0MwQoFDE7p-Bll4hps -s 'Sheet1!A1:G50' -f gsheet`

**Please note**: If you want to provide JSON user data that has empty values, such as empty strings or false values, then you must use the forceSendFields field (see [Empty Data Fields](empty_data.md)).

## batch-delete users

**Command aliases**:<br />
bdelete, bdel<br />
user, usrs, usr

**Flags**:<br />
--format (-f) input format (valid values: text, gsheet) text is the default<br />
--input-file (-i) Path to input file or Google Sheet ID<br />
--sheet-range (-s) Google sheet data range in the format 'Sheet1!A1:C10'


**Input data**: Google Sheet, Text file or piped text input

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-delete users command allows you to delete multiple Google Workspace users with one command. A message is displayed for each user that is deleted. If an error is encountered, the error is logged and displayed if the --silent flag is not being used. Processing continues with the next record.

The text input file, piped text input or Google Sheet must provide the email address or id of each user on a separate line like this:

    frank.castle@mycompany.com
    bruce.wayne@mycompany.com
    peter.parker@mycompany.com

**N.B.** Input Google Sheets must not have a header row.

**Examples**:<br />
`gmin bdel users -i /path/to/file/inputfile.txt`
`gmin batch-delete usrs -i 1zpyC6XzvTdKT5EIUywvqESX3A0MwQoFDE7p-Bll4hps -s 'Sheet1!A1:A50' -f gsheet`
`gmin ls user -a primaryemail -q orgunitpath=/TestOU | jq '.users[] | .primaryEmail' -r | gmin bdel user`

## batch-undelete users

**Command aliases**:<br />
bundelete, bund<br />
user, usrs, usr

**Flags**:<br />
--input-file (-i) Path to input file

**Input data**: Text input file or command line pipe

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-undelete users command allows you to undelete (restore) multiple Google Workspace users with one command. It can take an input file in plain text format or input from a command line pipe. A message is displayed for each user that is undeleted. If an error is encountered, processing stops and the error message is displayed.

The input file or piped input must provide the unique id of each user on a separate line like this:

    417578192529765228417
    308127142904731923463
    107967172367714327529

**Please note**: You must provide user ids and NOT email addresses. If you try to use email addresses you will see errors and the command will fail.

## batch-update users

**Command aliases**:<br />
bupdate, bupd<br />
user, usrs, usr

**Flags**:<br />
--input-file (-i) Path to input file

**Input data**: JSON input file

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-update users command allows you to update multiple Google Workspace users with one command. It takes an input file in JSON format. A message is displayed for each user that is updated. If an error is encountered, processing stops and the error message is displayed.

The input file must contain valid JSON. Details for each user are expected on separate lines like this:

## create user

**Command aliases**:<br />
crt<br />
usr  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The create user command allows you to create a Google Workspace user.

## delete user

**Command aliases**:<br />
del<br />
usr  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The delete user command allows you to delete a Google Workspace user.

## get user

**Command aliases**:<br />
usr

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user.readonly

## list users

**Command aliases**:<br />
ls<br />
user, usrs, usr

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user.readonly

## undelete user

**Command aliases**:<br />
und<br />
usr  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The undelete user command allows you to undelete a Google Workspace user.

## update user

**Command aliases**:<br />
upd<br />
usr  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The update user command allows you to update a Google Workspace user.