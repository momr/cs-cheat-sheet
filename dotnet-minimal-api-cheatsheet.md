# .NET Minimal API Cheat Sheet

## Table of Contents
1. [Introduction](#introduction)
2. [Basic Setup](#basic-setup)
3. [Routing](#routing)
4. [Request Handling](#request-handling)
5. [Response Handling](#response-handling)
6. [Dependency Injection](#dependency-injection)
7. [Middleware](#middleware)
8. [Authentication and Authorization](#authentication-and-authorization)
9. [OpenAPI (Swagger) Support](#openapi-swagger-support)
10. [Testing](#testing)

## Introduction

Minimal APIs in .NET provide a simplified approach to building HTTP APIs with less ceremony and minimal dependencies. They are ideal for microservices and apps that want to include only the minimum files, features, and dependencies.

[Official Documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis)

## Basic Setup

Create a new Minimal API project:

```bash
dotnet new web -n MyMinimalApi
```

Basic program structure (Program.cs):

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```

## Routing

```csharp
// GET request
app.MapGet("/api/items", () => "Getting all items");

// POST request
app.MapPost("/api/items", () => "Creating an item");

// PUT request
app.MapPut("/api/items/{id}", (int id) => $"Updating item {id}");

// DELETE request
app.MapDelete("/api/items/{id}", (int id) => $"Deleting item {id}");

// Route with multiple HTTP methods
app.MapMethods("/api/items", new[] { "HEAD", "PATCH" }, () => "HEAD or PATCH request received");

// Route groups
var apiGroup = app.MapGroup("/api");
apiGroup.MapGet("/items", () => "Getting all items");
apiGroup.MapGet("/users", () => "Getting all users");
```

## Request Handling

```csharp
// Route parameters
app.MapGet("/api/items/{id}", (int id) => $"Getting item {id}");

// Query parameters
app.MapGet("/api/items", (string? name, int? page) => 
    $"Getting items with name: {name}, page: {page}");

// Request body
app.MapPost("/api/items", (Item item) => $"Creating item: {item.Name}");

// Form data
app.MapPost("/api/upload", async (IFormFile file) =>
{
    using var stream = File.OpenWrite(file.FileName);
    await file.CopyToAsync(stream);
    return $"Uploaded: {file.FileName}";
});

// Headers
app.MapGet("/api/headers", (HttpRequest request) => 
    $"User-Agent: {request.Headers["User-Agent"]}");
```

## Response Handling

```csharp
// Returning different status codes
app.MapGet("/api/items/{id}", (int id) =>
    id < 1 ? Results.BadRequest("Invalid ID") : Results.Ok($"Item {id}"));

// Returning JSON
app.MapGet("/api/items", () => Results.Json(new { Name = "Item 1", Price = 9.99 }));

// Returning a file
app.MapGet("/api/file", () => Results.File("path/to/file.pdf", "application/pdf"));

// Redirecting
app.MapGet("/old-path", () => Results.Redirect("/new-path"));

// Customizing response headers
app.MapGet("/api/custom-header", () => Results.Text("Hello")
    .WithHeaders(new HeaderDictionary { { "X-Custom-Header", "Value" } }));
```

## Dependency Injection

```csharp
// Registering services
builder.Services.AddSingleton<IMyService, MyService>();

// Using dependency injection in endpoints
app.MapGet("/api/service-data", (IMyService myService) => myService.GetData());

// Scoped services
app.MapGet("/api/scoped", async (IServiceProvider sp) =>
{
    using var scope = sp.CreateScope();
    var scopedService = scope.ServiceProvider.GetRequiredService<IScopedService>();
    return await scopedService.GetDataAsync();
});
```

## Middleware

```csharp
// Adding middleware
app.Use(async (context, next) =>
{
    // Do something before the request
    await next();
    // Do something after the request
});

// Error handling middleware
app.Use(async (context, next) =>
{
    try
    {
        await next();
    }
    catch (Exception ex)
    {
        context.Response.StatusCode = 500;
        await context.Response.WriteAsync($"An error occurred: {ex.Message}");
    }
});

// Built-in middleware
app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseCors();
```

## Authentication and Authorization

```csharp
// Adding authentication
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer();

// Adding authorization
builder.Services.AddAuthorization();

app.UseAuthentication();
app.UseAuthorization();

// Secure an endpoint
app.MapGet("/api/secure", [Authorize] () => "This is a secure endpoint")
    .RequireAuthorization();

// Role-based authorization
app.MapGet("/api/admin", [Authorize(Roles = "Admin")] () => "Admin endpoint");

// Policy-based authorization
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("AdminPolicy", policy => policy.RequireRole("Admin"));
});

app.MapGet("/api/admin-policy", () => "Admin policy endpoint")
    .RequireAuthorization("AdminPolicy");
```

## OpenAPI (Swagger) Support

```csharp
// Add Swagger support
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

// Use Swagger
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

// Annotate endpoints
app.MapGet("/api/items", () => "Getting all items")
    .WithName("GetItems")
    .WithOpenApi();

// Add response types
app.MapGet("/api/items/{id}", (int id) => $"Getting item {id}")
    .Produces(StatusCodes.Status200OK)
    .Produces(StatusCodes.Status404NotFound)
    .WithOpenApi();
```

## Testing

```csharp
// In your test project
public class MinimalApiTests : IClassFixture<WebApplicationFactory<Program>>
{
    private readonly WebApplicationFactory<Program> _factory;

    public MinimalApiTests(WebApplicationFactory<Program> factory)
    {
        _factory = factory;
    }

    [Fact]
    public async Task GetItems_ReturnsSuccessStatusCode()
    {
        var client = _factory.CreateClient();

        var response = await client.GetAsync("/api/items");

        response.EnsureSuccessStatusCode();
    }
}
```

This cheat sheet covers the basics of creating and working with Minimal APIs in .NET, which provide a similar lightweight and fast approach to building HTTP APIs as FastAPI does in the Python world. Minimal APIs are particularly well-suited for microservices and simple HTTP APIs where you want to minimize overhead and dependencies.
