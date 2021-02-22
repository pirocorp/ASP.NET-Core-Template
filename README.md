# ASP.NET Core Template

A ready-to-use template for ASP.NET Core with repositories, services, models mapping, DI and StyleCop warnings fixed.

## Build status

[![Build Status](https://nikolayit.visualstudio.com/AspNetCoreTemplate/_apis/build/status/NikolayIT.ASP.NET-Core-Template?branchName=master)](https://nikolayit.visualstudio.com/AspNetCoreTemplate/_build/latest?definitionId=15&branchName=master)

## Authors

- [Nikolay Kostov](https://github.com/NikolayIT)
- [Vladislav Karamfilov](https://github.com/vladislav-karamfilov)
- [Stoyan Shopov](https://github.com/StoyanShopov)

## Package Installation

You can install this template using [NuGet](https://www.nuget.org/packages/AspNetCoreTemplate):

```powershell
dotnet new -i AspNetCoreTemplate
```

```powershell
dotnet new aspnet-core -n YourProjectName
```

## Pack this Template

```powershell
dotnet pack .\nuget.csproj
```

## Project Overview

![Dependencies Graph](https://user-images.githubusercontent.com/25417032/97107966-0e5fc500-16d3-11eb-9b9c-c73012ff97ac.png)
![image](https://user-images.githubusercontent.com/25417032/97108063-9fcf3700-16d3-11eb-8225-32eac21c4542.png)

### Common

**AspNetCoreTemplate.Common** contains common things for the project solution. For example:

- [GlobalConstants.cs](https://github.com/NikolayIT/ASP.NET-Core-Template/blob/master/src/AspNetCoreTemplate.Common/GlobalConstants.cs).

### Data

This solution folder contains three subfolders:

- AspNetCoreTemplate.Data.Common
- AspNetCoreTemplate.Data.Models
- AspNetCoreTemplate.Data

#### AspNetCoreTemplate.Data.Common

[AspNetCoreTemplate.Data.Common.Models](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Data/AspNetCoreTemplate.Data.Common/Models) provides abstract generics classes and interfaces, which holds information about our entities. For example when the object is Created, Modified, Deleted or IsDeleted. It contains a property for the primary key as well.

[AspNetCoreTemplate.Data.Common.Repositories](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Data/AspNetCoreTemplate.Data.Common/Repositories) provides two interfaces IDeletableEntityRepository and IRepository, which are part of the **repository pattern**.

#### AspNetCoreTemplate.Data.Models

[AspNetCoreTemplate.Data.Models](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Data/AspNetCoreTemplate.Data.Models) contains ApplicationUser and ApplicationRole classes, which inherits IdentityRole and IdentityUsers.

#### AspNetCoreTemplate.Data

[AspNetCoreTemplate.Data](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Data/AspNetCoreTemplate.Data) contains DbContext, Migrations and Configuraitons for the EF Core.There is Seeding and Repository functionality as well.

### Services

This solution folder contains four subfolders:

- AspNetCoreTemplate.Services.Data
- AspNetCoreTemplate.Services.Mapping
- AspNetCoreTemplate.Services.Messaging
- AspNetCoreTemplate.Services

#### AspNetCoreTemplate.Services.Data

[AspNetCoreTemplate.Services.Data](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Services/AspNetCoreTemplate.Services.Data) wil contains service layer logic.

#### AspNetCoreTemplate.Services.Mapping

[AspNetCoreTemplate.Services.Mapping](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Services/AspNetCoreTemplate.Services.Mapping) provides simplified functionlity for auto mapping. For example:

```csharp
using Blog.Data.Models;
using Blog.Services.Mapping;

public class TagViewModel : IMapFrom<Tag>
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

Or if you have something specific:

```csharp
using System;

using AutoMapper;
using Blog.Data.Models;
using Blog.Services.Mapping;

public class IndexPostViewModel : IMapFrom<Post>, IHaveCustomMappings
{
    public int Id { get; set; }

    public string Title { get; set; }

    public string Author { get; set; }

    public string ImageUrl { get; set; }

    public DateTime CreatedOn { get; set; }

    public void CreateMappings(IProfileExpression configuration)
    {
        configuration.CreateMap<Post, IndexPostViewModel>()
            .ForMember(
                source => source.Author,
                destination => destination.MapFrom(member => member.ApplicationUser.UserName));
    }
}

```

#### AspNetCoreTemplate.Services.Messaging

[AspNetCoreTemplate.Services.Messaging](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Services/AspNetCoreTemplate.Services.Messaging) a ready to use integration with [SendGrid](https://sendgrid.com/).

#### AspNetCoreTemplate.Services

[AspNetCoreTemplate.Services](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Services/AspNetCoreTemplate.Services)

### Tests

This solution folder contains three subfolders:

- AspNetCoreTemplate.Services.Data.Tests
- AspNetCoreTemplate.Web.Tests
- Sandbox

#### AspNetCoreTemplate.Services.Data.Tests

[AspNetCoreTemplate.Services.Data.Tests](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Tests/AspNetCoreTemplate.Services.Data.Tests) holds unit tests for our service layer with ready setted up xUnit.

#### AspNetCoreTemplate.Web.Tests

[AspNetCoreTemplate.Web.Tests](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Tests/AspNetCoreTemplate.Web.Tests) setted up Selenuim tests.

#### Sandbox

[Sandbox](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Tests/Sandbox) can be used to test your logic.

### Web

This solution folder contains three subfolders:

- AspNetCoreTemplate.Web.Infrastructure
- AspNetCoreTemplate.Web.ViewModels
- AspNetCoreTemplate.Web

#### AspNetCoreTemplate.Web.Infrastructure

[AspNetCoreTemplate.Web.Infrastructure](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Web/AspNetCoreTemplate.Web.Infrastructure) contains functionality like Middlewares and Filters.

#### AspNetCoreTemplate.Web.ViewModels

[AspNetCoreTemplate.Web.ViewModels](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Web/AspNetCoreTemplate.Web.ViewModels) contains objects, which will be mapped from/to our entities and used in the front-end/back-end.

#### AspNetCoreTemplate.Web

[AspNetCoreTemplate.Web](https://github.com/NikolayIT/ASP.NET-Core-Template/tree/master/src/Web/AspNetCoreTemplate.Web) self explanatory.

## Support

If you are having problems, please let us know by [raising a new issue](https://github.com/NikolayIT/ASP.NET-Core-Template/issues).

## Example Projects

- <https://github.com/NikolayIT/PressCenters.com>
- <https://github.com/NikolayIT/nikolay.it>

## License

This project is licensed with the [MIT license](LICENSE).

## Template Structure

* Data -> Data Layer
	* Data -> DbContext, Migrations, Entities Configuration, Repository Implementation, Raw query runner, Seeders, Database configurations, etc.
		* Configurations -> Domain model fluent api configurations (IEntityTypeConfiguration)
			* ApplicationUserConfiguration -> Identity user configuration
		* Migrations -> Migrations
		* Repositories -> Repository implementations
			* EfRepository -> Implements repository pattern. Implements IRepository. Can be used for in memory database for integration tests
			* EfDeletableEntityRepository -> Implements repository pattern for Entities which supports soft delete. Extends EfRepository and implements IDeletableEntityRepository
		* Seeding -> Seeders
			* ISeeder -> All seeders must implement ISeeder interface
			* RolesSeeder -> Seed roles (Only admin role by default), implements ISeeder
			* SettingsSeeder -> Seed settings
			* ApplicationDbContextSeeder -> Calls all seeders, implements ISeeder		
		* ApplicationDbContext -> Extends IdentityDbContext Override SaveChanges and SaveChangesAsync to apply ApplyAuditInfoRules
		* appsettings.json -> Settings for design time (ConnectionString while adding migrations)
		* DbQueryRunner -> Raw query runner implementation Implements IDbQueryRunner
		* DesignTimeDbContextFactory -> Design-time services will automatically discover implementations of this interface. It will be used for migrations with CLI or PMC
		* EfExpressionHelper -> 
		* EntityIndexesConfiguration -> Makes IsDeleted index for all IDeletableEntity entities 
		* IdentityOptionsProvider -> Confgure identity options (Password Length)
			
	* Data.Common -> Base Entity Models, Repository Interfaces, QueryRunner interface, etc.
		* Models -> Base Entity Models
			* BaseModel -> Implements IAuditInfo
				* IAuditInfo -> All entities which have CreatedOn and ModifiedOn properties must implement IAuditInfo interface
			* BaseDeletableModel -> inherits BaseModel and implements IDeletableEntity
				* IDeletableEntity -> all entities which supports soft delete must implement IDeletableEntity interface. They have IsDeleted and DeletedOn properties.
		* Repositories -> Interfaces for repository pattern
			* IRepository -> All reposiotry implementations must implement IRepository interface
			* IDeletableEntityRepository -> All repository implementations for entities which support soft delete must implement IDeletableEntityRepository
		* IDbQueryRunner -> All raw query runners must implement QueryRunner interface
		
	* Data.Models -> Models(Entities, Domain Models)
		* ApplicationRole -> Implements IdentityRole, IAuditInfo, IDeletableEntity (Supports soft delete)
		* ApplicationUser -> Implements IdentityUser, IAuditInfo, IDeletableEntity (Supports soft delete)
		* Setting -> Entity example, all entities should extend BaseDeletableModel or BaseModel. Extends BaseDeletableModel
		
* Services -> Service Layer
	* Services -> Helper services not directly linked to the database
	
	* Services.Data -> Services and services interfaces for managing data in database
		* ISettingsService -> Interface for SettingsService
		* SettingsService -> SettingsService implements ISettingsService
		
	* Services.Mapping -> AutoMapper configuration
		* IMapFrom -> All projections from database to custom classes must implement IMapFrom
		* IMapTo -> All input models must implement IMapTo
		* IHaveCustomMappings -> All projections with custom mappings must implement IHaveCustomMappings
		* AutoMapperConfig -> Loads all mappings and stores automapper instance (IMapper MapperInstance)
		* QueryableMappingExtensions -> AutoMapper extension method To with no need to provide ConfigurationProvider
		
	* Services.Messaging -> E-mail Sender, etc.
		* IEmailSender -> All Email sender implementations must implement IEmailSender
		* NullMessageSender -> Don't actualy send email just returns CompletedTask implements IEmailSender
		* EmailAttachment -> Defines email attachment object
		* SendGridEmailSender -> Actual email sender implementation implements IEmailSender
	
* Web -> Presentation Layer
	* Web -> ASP.NET Core MVC, in Startup class is DI container, default startup project, appsettings.json
		* Areas -> Areas organize related functionality into a group as a separate namespace
			* Administration -> MVC area
			* Identity -> Razor pages area
		* Controllers -> Controllers not belonging to any particular area
			* BaseController -> Common controllers logic
		* Views -> Views 
			* Shared -> Layout and global partials 
				* _CookieConsentPartial -> cookie consent partial view
				* _Layout -> Layout
				* _LoginPartial -> login partial view
				* Error -> Error view
			* _ViewImports -> Specifies global usings and tag helpers for views
			* _ViewStart -> Specifies default layout for views
		* wwwroot -> Statc files are stored here (js, css, etc)
		* appsettings.json -> Global app settings
		* appsettings.Development.json -> App settings for specific for environment Development
		* bundleconfig.json -> Minification and bundling configuration
		* libman -> Client side libraries configuration
		* Program -> Application entry point.
		* Startup -> Application configuration (Services, Middlewares, Filters, etc.)
		
	* Web.Infrastructure -> Helpers, etc.
	
	* Web.ViewModels -> View Models, etc.
		* ErrorViewModel - Error view model
	
* Tests -> Test Projects
	* Services.Data.Tests -> Project with tests for services
		* SettingsServiceTests -> Tests for Settings Service
		
	* Web.Tests -> Selenium Tests
		* SeleniumServerFactory ->
		* SeleniumTests -> UI tests,
		* WebTests ->
		
	* Sandbox -> Console Sandbox for testesting purposes
	
* Common -> Global Constants, etc
	* GlobalConstants -> Contains global constants (AdministratorRoleName)
	
* Rules.ruleset -> StyleCop ruleset
* Settings.StyleCop -> StyleCop settings
* stylecop.json -> More StyleCop settings

## Notes
* Migrations should be applied through PowerShell e.g. dotnet ef migrations add MigrationName
* Controllers must inherit BaseController 
