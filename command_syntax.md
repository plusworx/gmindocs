# Command Syntax
The gmin command syntax has been designed to be reasonably intuitive and consistent. Commands usually take the form of `gmin <verb> <object> [arguments] [flags]`. Although there may be the odd exception like `gmin whoami`.

## Flags
Command flags can have short names like **-x** and long names like **--longnameforx** and they can take an accompanying argument. They can be used with or without an equals sign so that:

`--first-name=George` is equivalent to `--first-name George`. However, flags that relate to boolean values (true/false) have a slightly different syntax. An equals sign **must** be used if a value is provided so that:

`-c=true` or `-c=false` is correct, but `-c true` is not and will be interpreted incorrectly.

You can set a boolean flag to true by providing the flag on its own like this:

`-c` or `--change-password` but this only works for true and **not** for false.

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