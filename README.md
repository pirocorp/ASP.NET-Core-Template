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
		* Configurations -> Domain model fluent api configurations (IEntityTypeConfiguration)
			* ApplicationUserConfiguration -> Identity user configuration
		* Migrations -> Migrations
		* Repositories -> Repository implementations
			* EfRepository -> Implements repository pattenr. Implements IRepository
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
				* IAuditInfo -> All entities which have CreatedOn and ModifiedOn must implement IAuditInfo interface
			* BaseDeletableModel -> inherits BaseModel and implements IDeletableEntity
				* IDeletableEntity -> all entities which supports soft delete must implement IDeletableEntity interface
		* Repositories -> Interfaces for repository pattern
			* IRepository -> All reposiotry implementations must implement IRepository interface
			* IDeletableEntityRepository -> All repository implementations for entities which support soft delete must implement IDeletableEntityRepository
		* IDbQueryRunner -> All raw query runners must implement QueryRunner interface
		
	* Data.Models -> Models(Entities, Domain Models)
		* ApplicationRole -> Implements IdentityRole, IAuditInfo, IDeletableEntity (Supports soft delete)
		* ApplicationUser -> Implements IdentityUser, IAuditInfo, IDeletableEntity (Supports soft delete)
		* Setting -> Extends BaseDeletableModel
		
* Services -> Service Layer
	* Services -> 
	
	* Services.Data -> Services and services interfaces for managing data in database
		* ISettingsService -> Interface for SettingsService
		* SettingsService -> SettingsService implements ISettingsService
		
	* Services.Mapping -> AutoMapper configuration
		* IMapFrom -> All projections must implement IMapFrom
		* IMapTo -> All sources must implement IMapTo
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
		* SeleniumTests ->
		* WebTests ->
	* Sandbox -> Console Sandbox
	
* Common -> Global Constants, etc
	* GlobalConstants -> Contains global constants (AdministratorRoleName)
	
* Rules.ruleset -> StyleCop ruleset
* Settings.StyleCop -> StyleCop settings
* stylecop.json -> More StyleCop settings

## Notes
* Migrations should be applied through PowerShell e.g. dotnet ef migrations add MigrationName
* Controllers must inherit BaseController 