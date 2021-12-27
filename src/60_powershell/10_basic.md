* ```get-help <command>```
* ```get-command```
* ```get-command -noun "*Time"``` - find command with noun Time
* ```get-command -Module AWSPowershell``` - find command in AWSPowershell module

* ```get-process```
* ```get-service```

###Modules
* ```get-module``` module added to my session
* ```get-module -listavaiable``` - downloaded and ready to import
* ```find-module Az``` find module "Az"
* ```install-module Az``` install module "Az"
* ```import-module Az``` add to session "Az"
* ```get-command -modue Az.sql``` available command for module Az.sql
 

####Chaining commends
* ```get-process | select-process ProcessName``` return process name column
* ```get-process | select-process ProcessName | Sort-Object ProcessName``` 
* ```get-process | where {$.ProcessName -eq "systemd""}``` 

####Conditionals
* ```if ($myVar.CPU -gt 1) {Write-Host "Works"} else {Write-Host "Nothing"}``` 

####script
* use file with extension *.ps1
* run script ```./psscript.ps1```
* run from bash ```pwsh psscript.ps1``



