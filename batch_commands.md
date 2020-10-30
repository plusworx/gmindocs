# Batch Commands

gmin batch commands are used to perform bulk operations. They are useful when you want to perform a number of similar operations using one command.

There are several batch commands and they all have aliases that save you some typing. They are as follows:

* **batch-create** (bcreate, bcrt)
* **batch-delete** (bdelete, bdel)
* **batch-manage** (bmanage, bmng)
* **batch-move** (bmove, bmv)
* **batch-undelete** (bundelete, bund)
* **batch-update** (bupdate, bupd)

Batch commands can accept input data from pipes as well as text, CSV files and Google Sheets. This means that you can do things like:

`gmin ls user -a primaryemail -q orgunitpath=/TestOU | jq '.users[] | .primaryEmail' -r | gmin bdel user`

The above gmin list command returns a list of primary email addresses for users who belong to the TestOU orgunit. The result of this query is returned as JSON which is piped into a jq command that is used to get the raw email addresses which in turn, are piped into the gmin batch-delete command which deletes those users.

See the 'Managing ...' sections of the documentation to get information on how these batch commands are applied to Google Workspace objects.