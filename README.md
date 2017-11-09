# ASP.NET Core 2 Notes

## Overview
* Backed by processing pipeline that can be added to.
* Supports DI natively.
* Test through xUnit.Net
* NuGet for package management.

## Console app

Using command line a simple console application can be created by:
```
dotnet --version

dotnet --help

dotnet new console

dotnet run
```
## Web

```
dotnet new mvc
```

* Uses bower for front ent package management.  
* This command can be replicated in VS.
* Two options for running in VS, using sql express of using kestrel.
* Web host connected to controllers and a simple http processing.

Use:
```
app.UseDefaultFiles();
app.UseStaticFiles();
```
to allow serving static files.

* Controllers do the work and return. 
* Each public method in a controller is an action.  
* Return View will return the view matching the method name.  These are Razor views.  Unless you change the view returned using
```
public IActionResult About()
{
	return View("Info");
}
```

* ViewData is a dictionary to pass data from the controller into the view.
* Everything after the host:port is <Controller>/<Action> e.g.
```
localhost:9876/Home/About
```
The views are linked to the folder structure in the views folder. e.g.
```
Views\Home\About.cshtml
```

* Uses routing to map URL pattern to the controller and action

## Restful Services

```
dotnet new webapi
```

* Map HTTP verbs to CRUD
|HTTP|CRUD|
|----|----|
|POST | **C**reate |
|GET | **R**ead|
|PUT | **U**pdate|
|DELTE|**D**elete|

* Use HTTP response codes to map to Restful meanings,i.e. 201 = Created = New resource created
* Use existing technologies, HTTP, URIs, XML, JSON etc
* Focus on resources 
* Controllers provide methods that that return resources
* Can add xml return output by adding it to the mvc
* Use Json decorators from Newton soft to add serialisation directives.
* Using the repository pattern enables swapping the repository.
* Use IActionResult to allow return of either the correct object or generic results such as NoContent() or BadRequest()
* Add swagger to controller to allow easier development
```
NuGet
swashbuckle.aspnetcore
```

* Link to instructions on adding swagger is [here](https://elanderson.net/2017/10/swagger-and-swashbuckle-with-asp-net-core-2/)
* Edit launchsettings.json to change the startup options for a project
* use colons on inputs to ensure type is adhered to:
```
 [httpGet("id:int")]
```

## Dependency Injection
* No part of .net core but quite limited.  Only one public constructor can use dependency injection.
* 3 modes of operation - Transient (every request new object), Singleton (Every request same object), Scoped (Every request in same session gets same object)

## Config
* Config can be set in INI, JSON or XML files.  Default is JSON e.g. appsettings.json.
* Configs are added in program.cs and can add lots of values into a key value pair:
```
builder.AddJsonFile("config.json", optional: true, reloadOnChange: true)
                                .AddXmlFile("config.xml", optional: true, reloadOnChange: true)
                                .AddIniFile("config.ini", optional: true, reloadOnChange: true)
                                .AddEnvironmentVariables()
                                .AddCommandLine(new string[] { "locale=en-gb", "superuser=true" });
```

## Entity Framework
* Alternatives 
  * Dapper



