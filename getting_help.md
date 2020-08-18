# Getting Help

## help flag
The help flag (--help or -h) can be used with any gmin command to display built-in help text. The more specific the command, the more specific help information. For instance, if you type `gmin -h` then you will get very high level and generalised help. However, if you type something like `gmin ls users -h` then you will get much more specific help about listing users.

## show command

### show config
The `gmin show config` command will display any gmin environment variables that are set, as well as contents of a configuration file if one exists. 

### show attributes

**Command aliases**:<br />
attrs

**Flags**:<br />
--composite (-c) Show fields that contain other fields<br />
--filter (-f) Show fields whose names contain the filter string<br />
--queryable (-q) Show fields that can be used with the query flag<br />

The `gmin show attributes` command allows you to display field names (attributes) of G Suite objects.

**Examples**:

`gmin show attrs user`<br />
This would show you all of the field names for the user object. You will notice that some fields have an asterisk (*) next to them. This denotes fields that are composite fields, meaning that they are arrays or fields that are made up of other fields.

`gmin show attrs user -c`<br />
This would get a list of all of the composite fields within the user object.

`gmin show attrs user address`<br />
 This would display the fields within an address.

`gmin show attrs user -q`<br />
This would display a list of user fields can be used with the list command query flag. **Please note**: you cannot use the --queryable and --composite flags in the same command.

`gmin show attrs user -f ssh`<br />
This would display all of the user fields that contain the string 'ssh' in their names.

### show attribute-values
`gmin show attribute-values`

### show flag-values
`gmin show flag-values`

## whoami command

The `gmin whoami` command will display the admin user email address that gmin is impersonating to perform tasks.