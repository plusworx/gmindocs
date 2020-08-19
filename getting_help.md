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

**Valid objects**:<br />
chromeosdevice, crosdevice, cdev<br />
group, grp<br />
group-alias, grp-alias, galias, ga<br />
group-member, grp-member, grp-mem, gmember, gmem<br />
orgunit, ou<br />
schema, sc<br />
user<br />
user-alias, ualias, ua<br />

The `gmin show attributes` command allows you to display field names (attributes) of G Suite objects.

**Examples**:

`gmin show attrs user`<br />
This command shows you all of the field names for the user object. You will notice that some fields have an asterisk (*) next to them. This denotes fields that are composite fields, meaning that they are arrays or fields that are made up of other fields.

`gmin show attrs user -c`<br />
This command gets a list of all of the composite fields within the user object.

`gmin show attrs user address`<br />
 This command displays the fields within an address.

`gmin show attrs user -q`<br />
This command displays a list of user fields that can be used with the list command query flag. **Please note**: you cannot use the --queryable and --composite flags in the same command.

`gmin show attrs user -f ssh`<br />
This command displays all of the user fields that contain the string 'ssh' in their names.

### show attribute-values

**Command aliases**:<br />
attr-vals, avals

**Valid objects**:<br />
chromeosdevice, crosdevice, cdev<br />
group-member, grp-member, grp-mem, gmember, gmem<br />
user<br />

The `gmin show attribute-values` command allows you to discover predefined values for object fields (attributes).

**Examples**:

`gmin show avals user`
This command displays all of the user fields that have predefined values.

`gmin show attribute-values user email type`
This command displays the predefined values for the type field in the user email attribute.

### show flag-values

**Command aliases**:<br />
flag-vals, fvals

**Valid objects**:<br />
chromeosdevice, crosdevice, cdev<br />
group, grp<br />
group-member, grp-member, grp-mem, gmember, gmem<br />
orgunit, ou<br />
user<br />

The `gmin show flag-values` command allows you to discover predefined values for command flags.

**Examples**:

`gmin show fvals user`
This command displays the names of the flags that have predefined values that can be used with user object commands.

`gmin show fvals user orderby`
This command displays the predefined values for the orderby flag when used with user object commands.

## whoami command

The `gmin whoami` command will display the admin user email address that gmin is impersonating to perform tasks.