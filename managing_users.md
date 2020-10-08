# Managing Users

This section contains information about the commands that you can use to manage Google Workspace users.

## batch-create users

**Command aliases**:<br />
bcreate, bcrt<br />
user

**Flags**:<br />
--inputfile (-i) Path to input file

**Input data**: JSON input file

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-create users command allows you to create multiple Google Workspace users with one command. It takes an input file in JSON format and outputs a message for each user that it creates. If an error is encountered, processing stops and an error message is displayed.

The input file must contain valid JSON. Details for each user are expected on separate lines like this:

    {"name":{"firstName":"Stan","familyName":"Laurel"},"primaryEmail":"stan.laurel@company.com","password":"SecretPassword",changePasswordAtNextLogin":true}
    {"name":{"givenName":"Oliver","familyName":"Hardy"},"primaryEmail":"oliver.hardy@company.com","password":"SecretPassword","changePasswordAtNextLogin":true}
    {"name":{"givenName":"Harold","familyName":"Lloyd"},"primaryEmail":"harold.lloyd@company.com","password":"SecretPassword","changePasswordAtNextLogin":true}

**Example**:<br />
`gmin bcrt users -i /path/to/file/inputfile.json`

**Please note**: If you want to provide user data that has empty values, such as empty strings or false values, then you must use the forceSendFields field (see [Empty Data Fields](empty_data.md)).

## batch-delete users

**Command aliases**:<br />
bdelete, bdel<br />
user

**Flags**:<br />
--inputfile (-i) Path to input file

**Input data**: Text input file or command line pipe

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-delete users command allows you to delete multiple Google Workspace users with one command. It can take an input file in plain text format or input from a command line pipe. A message is displayed for each user that is deleted. If an error is encountered, processing stops and the error message is displayed.

The input file or piped input must provide the email address or id of each user on a separate line like this:

    frank.castle@mycompany.com
    bruce.wayne@mycompany.com
    peter.parker@mycompany.com

**Examples**:<br />
`gmin bdel users -i /path/to/file/inputfile.txt`
`gmin ls user -a primaryemail -q orgunitpath=/TestOU | jq '.users[] | .primaryEmail' -r | gmin bdel user`

## batch-undelete users

**Command aliases**:<br />
bundelete, bund<br />
user

**Flags**:<br />
--inputfile (-i) Path to input file

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
user

**Flags**:<br />
--inputfile (-i) Path to input file

**Input data**: JSON input file

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The batch-update users command allows you to update multiple Google Workspace users with one command. It takes an input file in JSON format. A message is displayed for each user that is updated. If an error is encountered, processing stops and the error message is displayed.

The input file must contain valid JSON. Details for each user are expected on separate lines like this:

## create user

**Command aliases**:<br />
crt  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The create user command allows you to create a Google Workspace user.

## delete user

**Command aliases**:<br />
del  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The delete user command allows you to delete a Google Workspace user.

## get user

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user.readonly

## list users

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user.readonly

## undelete user

**Command aliases**:<br />
und  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The undelete user command allows you to undelete a Google Workspace user.

## update user

**Command aliases**:<br />
upd  

**Required Scope**: https://www.googleapis.com/auth/admin.directory.user

The update user command allows you to update a Google Workspace user.