# ASP.NET Core Template

A ready-to-use template for ASP.NET Core with repositories, services, models mapping, DI and StyleCop warnings fixed.

## Build status

[![Build Status](https://nikolayit.visualstudio.com/AspNetCoreTemplate/_apis/build/status/NikolayIT.ASP.NET-Core-Template?branchName=master)](https://nikolayit.visualstudio.com/AspNetCoreTemplate/_build/latest?definitionId=15&branchName=master)

## Authors

- [Nikolay Kostov](https://github.com/NikolayIT)
- [Vladislav Karamfilov](https://github.com/vladislav-karamfilov)


## Template Structure

* Data -> Data Layer
	* Data
	* Data.Common
	* Data.Models	
	
* Services -> Service Layer
	* Services
	* Services.Data
	* Services.Mapping
	* Services.Messaging
	
* Web -> Presentation Layer
	* Web
	* Web.Infrastructure
	* Web.ViewModels
	
* Tests
	* Services.Data.Tests
	* Web.Tests
	* Sandbox
	
* Common