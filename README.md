# ProductAPI_EF

- This is a simple web api for product/order management built using ASP.NET CORE Web API 5.0.

- CRUD operation for Product and Customer has been implemented.

- Entity Framework Core has been used to work with the database.

- DB First Approach has been implemented. Database first approach means the database is already existing, all we have to do is to generate entity classes for the tables you want to work with.

Steps:
- Create a database and two tables inside it; products and customers
- create an asp.net core web api project ProductAPI_EF
- Use Entity Framework Core.

  - This framework is based on ORM(Object Relational Mapping) pattern that maps class and its properties with table and its columns in database.
  - We need to install this framework as a Nuget Package as it does not come installed by default2.
  - Steps to follow for installing packages:
		  solution Explorer -> Right click -> Manage Nuget package -> Browse -> Entityframework core
		    Microsoft.EntityFrameworkCore.Design
		    Microsoft.EntityFrameworkCore.Tools
		    Microsoft.EntityFrameworkCore
		    Microsoft.EntityFrameworkCore.SqlServer
		
		Note: choose version 3.1.20 for the above packages if using .netcore 3.1

- Fire the command to generate Entity classes (ORM classes, mapped to table in db)
  - Tools -> Nuget package manager -> Package manager console
  - Scaffold-DbContext "server=<servername>;database=<dbname>;integrated security=true" -OutputDir Models\EF -Provider Microsoft.EntityFrameworkCore.SqlServer
    (Check the models folder, it will have, EF folder now and a Model folder mapped to your table in database and properties mapped to columns in that table)
    
    Note: In DbContext class, you will see connection strings defined within OnConfiguring() method. Ensure to replace the connection strings with the connectionStrings name that represents connection string defined in appsettings.json file.
  
    ```C#
  
    if (!optionsBuilder.IsConfigured)
            {
                var builder = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true);
                IConfigurationRoot configuration = builder.Build();
                string connectionString = configuration.GetConnectionString("TrainingDBConnection");
               // optionsBuilder.UseSqlServer("Server=<servername>;Database=<dbname>;integrated security=true");
                optionsBuilder.UseSqlServer(connectionString);

            }
  
    ```

- Right click on controller folder, add new controller, choose API controller with actions using EF
 
 - This will create a new controller in the controller folder
 - Create two controllers, Customer and Product.
 - Instantiate DBContext class as we will work with it in order to work with the database.
  - Now build and run the project.
  - Test each GET, GET{id} POST, PUT, DELETE action and see if it works or not.
  - Hurray! We are done with our WEB API for managing customers and products.
  - The URL for this api can be shared for consumption via client technology.
  






