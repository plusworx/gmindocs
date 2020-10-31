# Managing ChromeOS Devices

This section contains information about the commands that you can use to manage ChromeOS devices in Google Workspace.

## batch-manage chromeos-devices

The batch-manage chromeos-devices command allows you to perform management actions on multiple Google Workspace managed ChromeOS devices. Valid actions are:

* deprovision
* enable
* reenable

**Command aliases**:<br />
bmanage, bmng<br />
chromeos-device, cros-devices, cros-device, cros-devs, cros-dev, cdevs, cdev

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --format | -f | string | input format (valid values: csv, gsheet, json) json is the default |
| --input-file | -i | string | Path to input file or Google Sheet ID |
| --sheet-range | -s | string | Google sheet data range in the format 'Sheet1!A1:C25' |

## batch-move chromeos-devices

The batch-move chromeos-devices command allows you to move multiple Google Workspace managed ChromeOS devices to different orgunits.

**Command aliases**:<br />
bmove, bmv<br />
chromeos-device, cros-devices, cros-device, cros-devs, cros-dev, cdevs, cdev

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --format | -f | string | input format (valid values: csv, gsheet, json) json is the default |
| --input-file | -i | string | Path to input file or Google Sheet ID |
| --sheet-range | -s | string | Google sheet data range in the format 'Sheet1!A1:B25' |

## batch-update chromeos-devices

The batch-update chromeos-devices command allows you to update information for multiple Google Workspace managed ChromeOS devices.

**Command aliases**:<br />
bupdate, bupd<br />
chromeos-device, cros-devices, cros-device, cros-devs, cros-dev, cdevs, cdev

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --format | -f | string | input format (valid values: csv, gsheet, json) json is the default |
| --input-file | -i | string | Path to input file or Google Sheet ID |
| --sheet-range | -s | string | Google sheet data range in the format 'Sheet1!A1:E25' |

## get chromeos-device

The get chromeos-device command retrieves information about a particular Google Workspace managed ChromeOS device.

**Command aliases**:<br />
chromeos-device, cros-device, cros-dev, cdev

**Arguments**<br />
device-id

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --attributes | -a | string | required device attributes |
| --projection | -j | string | type of projection (how much data to display) |

## list chromeos-devices

The list chromeos-devices command retrieves information about multiple Google Workspace managed ChromeOS devices.

**Command aliases**:<br />
ls<br />
chromeos-device, cros-devices, cros-device, cros-devs, cros-dev, cdevs, cdev

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --attributes | -a | string | required device attributes (separated by ~) |
| --count | | boolean | count number of entities returned |
| --max-results | -m | number | maximum number of results to return per page |
| --order-by | -o | string | field by which results will be ordered |
| --pages | -p | string | number of pages of results to be returned ('all' or a number) |
| --projection | -j | string | type of projection (how much data to display) |
| --query | -q | string | selection criteria to get devices (separated by ~) |
| --sort-order | -s | string | sort order of returned results |
| --orgunit-path | -t | string | sets orgunit path that returned devices belong to |

## manage chromeos-device

The manage chromeos-device command allows you to perform management actions on a particular Google Workspace managed ChromeOS device.

**Command aliases**:<br />
mng<br />
chromeos-device, cros-device, cros-dev, cdev

**Arguments**<br />
device-id<br />
action

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --reason | -r | string | device deprovision reason |

## move chromeos-device

The move chromeos-device command allows you to move a particular Google Workspace managed ChromeOS device to a different orgunit.

**Command aliases**:<br />
mv<br />
chromeos-device, cros-device, cros-dev, cdev

**Arguments**
device-id<br />
orgunitpath

## update chromeos-device

The update chromeos-device command allows you to update information for a particular Google Workspace managed ChromeOS device.

**Command aliases**:<br />
upd<br />
chromeos-device, cros-device, cros-dev, cdev

**Arguments**<br />
device-id

**Flags**

| Name | Short name | Type | Description |
|------|------------|------|-------------|
| --asset-id | -d | string | device asset id |
| --projection | -j | string | type of projection (how much data to display) |
| --location | -l | string | device location |
| --notes | -n | string | notes about device |
| --orgunit-path | -t | string | orgunit device belongs to |
| --user-key | -u | string | device user |