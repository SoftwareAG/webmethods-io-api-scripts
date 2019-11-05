# webmethods-io-api-scripts
Scripts for working with webMethods.io API
- `Export-Api.ps1` : Export a specific API version into the file system, e.g. to place it under version control for CI/CD

## Installation
Copy files to a location of your choice, preferably one that is part of the search path.

## API Export

Export a specific API version into the file system, e.g. to place it under version control for CI/CD

### Usage

Go the directory into which you want to have the API assets be placed. 

```
Export-Api [ {-Tenant <TENANT NAME> | -BaseUrl <BASE URL OF REST API>} 
	-Username <USERNAME> -Password <PASSWORD> 
	[-CreateConfigFile] [-ConfigFileName <NAME OF CONFIG FILE>]
	-ApiName <API NAME> -ApiVersion <API VERSION> ] 
	[-Verbose]
```

Options
- `-Tenant` : The following base URL will be used: `https://<TENANT NAME>.gateway.webmethodscloud.com/rest/apigateway`. This is mutually exclusive with the `-BaseUrl` option.
- `-BaseUrl` : Specify an arbitrary base URL. This is mutually exclusive with the `-Tenant` option.
- `-Username` : Username to login with
- `-Password` : Password for username. Use single-quotes, if it contains special characters (incl. space)
- `-CreateConfigFile` : Create configuration file in current directory
- `-ConfigFileName` : Use custom name for creation of configuration file (default = .sag-cloud-api in current directory)
- `-ApiName` : API name to search for
  - Use quotes, if it contains spaces
  - Supports wildcards
- `-ApiVersion` 
- `-Verbose` : In verbose mode the following information will be written to STDOUT
  - Search parameters: Tenant, username, API name, API version
  - Body of search request in JSON format
  - Search result in JSON format
  - UUID of API
  - URI to trigger export

In non-verbose mode the script writes the UUID of the API to STDOUT.  

### Examples

```
Export-Api -Tenant foobar 
	-Username user1 -Password 'secret' 
	-CreateConfigFile 
	-ApiName TestAPI -ApiVersion "1.0"
```
Will store the provided values in a configuration file in the current directory and then perform the export of the specified API and version. The UUID of the exported API will be written to the console.

```
Export-Api -Verbose
```
Read configuration file from current directory and perform the export with verbose output.


______________________
These tools are provided as-is and without warranty or support. They do not constitute part of the Software AG product suite. Users are free to use, fork and modify them, subject to the license agreement. While Software AG welcomes contributions, we cannot guarantee to include every contribution in the master project.

Contact us at [TECHcommunity](mailto:technologycommunity@softwareag.com?subject=Github/SoftwareAG) if you have any questions.
