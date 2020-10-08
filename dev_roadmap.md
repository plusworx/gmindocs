# Development Roadmap

## Documentation
* Built-in help - ongoing
* Docs website - ongoing

## Configuration
* ~~Enable use of environment variables~~ implemented in v0.5.0
* Integration with secrets managers like Google Secrets Manager or Hashicorp Vault
* ~~Granular setting of config file data~~ - implemented in v0.4.0 as set command.
* Switch service account JSON credentials

## API Functionality
### Admin SDK
**Data Transfer API**

**Directory API**
* ~~ChromeOS Devices~~ - implemented in v0.5.0
* Customers
* Domain Aliases
* Domains
* ~~Group Aliases~~ - implemented in v0.4.0
* ~~Mobile Devices~~ - implemented in v0.7.0
* Notifications
* Privileges
* Resources
* Role Assignments
* Roles
* ~~Schemas~~ - implemented in v0.6.0
* Tokens
* ~~User Aliases~~ - implemented in v0.4.0
* User Photos
* Verification Codes

**Reports API**

### Group Settings API ###
* Allow management of group settings

### Google Sheets API ###
* Allow reading of Google Sheets for batch command input

## General Functionality
* ~~Enable pipe input to batch commands~~ - implemented in v0.6.0
* ~~Enable .csv file input to batch commands~~ - implemented in 0.7.0
* ~~Enable Google Sheet input to batch commands~~ - implemented in 0.7.0
* ~~List pagination~~ - implemented in v0.5.0
* ~~Additional help with show function for valid attributes and types~~ implemented in v0.6.0
* ~~Show object attributes, enumerated object attribute values and enumerated command flag values~~ implemented in v0.7.0
* Enable command dry run
* Deletion confirmation
* Always on logging