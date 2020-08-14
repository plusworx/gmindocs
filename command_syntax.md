# Command Syntax
The gmin command syntax has been designed to be reasonably intuitive and consistent. Commands usually take the form of `gmin <verb> <object> [arguments] [flags]`. Although there may be the odd exception like `gmin whoami`.

## Flags
Command flags look like **-x** or **--longnameforx** and they take an accompanying argument. However, flags that relate to boolean values (true/false) just need the flag to be provided with no accompanying argument. For example, the **-c** or **--changepassword** flag when creating or updating a user.

Some flags are mutually exclusive and others are interdependent. Where this is the case, an error is displayed to explain what is required.

Type `gmin <command> -h or --help` to get help about a particular command. For example, to get help about creating a new user you could enter `gmin create user -h`.

## Flags that take multiple arguments
Get and list commands can have flags that have multiple arguments and where that is the case, the arguments are separated by the '~' symbol. If you only wanted to display particular fields when getting a list of users then you would specify those fields with an attribute flag and arguments like this:

`gmin ls users -a field1~field2~field3`

## Abbreviations or Aliases
Command elements can be abbreviated and these abbreviations or aliases are displayed in the help text. Some examples are:

**batch-create** -> **bcrt**<br />
**group-member** -> **gmem**<br />
**list** -> **ls**<br />
**orgunit** -> **ou**<br />
**user-alias** -> **ua**<br />

## Arguments that need to be quoted
When providing arguments that contain spaces or certain special characters you will need to surround them with single or double quotes. Arguments that are JSON strings will need to be surrounded with single quotes.