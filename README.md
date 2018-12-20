# Swashbuckle Behind NGINX Reverse Proxy Example

Running an ASP.NET Core WebAPI application behind a NGINX reverse proxy was challenging so I put toget her a sample in case it helps anyone else. This solution is just a 

    dotnet new webapi

Project with Swashbuckle added to it so you can see the ValuesController.

The main piece is in the Configure method
```csharp
    app.UseSwagger(c => {
        //change the path to include /api
        c.RouteTemplate = "/api/swagger/{documentName}/swagger.json";
    });

    app.UseSwaggerUI(c =>
    {
        //Notice the lack of / making it relative
        c.SwaggerEndpoint("swagger/v1/swagger.json", "My API V1");
        //This is the reverse proxy address
        c.RoutePrefix = "api";
    });
```

The three comments point out the changes necessary. Check out my blog for more details https://lukerogers.com/2018/12/20/swachbuckle-behind-nginx-reverse-proxy