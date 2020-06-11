# ASP.NET Core Template

A ready-to-use template for ASP.NET Core with repositories, services, models mapping, DI and StyleCop warnings fixed.

## Build status

[![Build Status](https://nikolayit.visualstudio.com/AspNetCoreTemplate/_apis/build/status/NikolayIT.ASP.NET-Core-Template?branchName=master)](https://nikolayit.visualstudio.com/AspNetCoreTemplate/_build/latest?definitionId=15&branchName=master)

## Authors

- [Nikolay Kostov](https://github.com/NikolayIT)
- [Vladislav Karamfilov](https://github.com/vladislav-karamfilov)


## Template Structure

* Data -> Data Layer
	* Data -> DbContext, Migrations, Entities Configuration, Repository Implementation, Raw query runner, Seeders, Database configurations, etc.
	* Data.Common -> BaseModel, Repository Interfaces, QueryRunner interface, etc.
	* Data.Models -> Models(Entities)
	
* Services -> Service Layer
	* Services -> External services
	* Services.Data -> Services and services interfaces for managing data in database
	* Services.Mapping -> AutoMapper configuration and custom interfaces
	* Services.Messaging -> E-mail Sender, etc.
	
* Web -> Presentation Layer
	* Web -> ASP.NET Core MVC, in Startup class is DI container, default startup project, appsettings.json
	* Web.Infrastructure -> Helpers, etc.
	* Web.ViewModels -> View Models, etc.
	
* Tests -> Test Projects
	* Services.Data.Tests -> Project with tests for services
	* Web.Tests -> Project with tests for ASP.NET Core MVC
	* Sandbox -> Sandbox
	
* Common -> Global Constants, etc

## Notes
* Migrations should be applied through PowerShell e.g. dotnet ef migrations add MigrationName
* Controllers must inherit BaseController 