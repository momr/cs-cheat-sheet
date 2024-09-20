# C# Tooling Cheat Sheet

## Table of Contents
1. [.NET CLI Tools](#net-cli-tools)
2. [Visual Studio Code Extensions](#visual-studio-code-extensions)
3. [NuGet Package Manager](#nuget-package-manager)
4. [Project Templates](#project-templates)
5. [Build Tools](#build-tools)
6. [Testing Tools](#testing-tools)
7. [Code Analysis Tools](#code-analysis-tools)
8. [Debugging Tools](#debugging-tools)
9. [Performance Profiling](#performance-profiling)
10. [Containerization and Deployment](#containerization-and-deployment)

## .NET CLI Tools

The .NET CLI (Command Line Interface) is a cross-platform toolchain for developing, building, running, and publishing .NET applications.

```bash
# Create a new console application
dotnet new console -n MyConsoleApp

# Create a new web application
dotnet new web -n MyWebApp

# Restore dependencies
dotnet restore

# Build the project
dotnet build

# Run the application
dotnet run

# Publish the application
dotnet publish -c Release

# Add a NuGet package
dotnet add package Newtonsoft.Json

# Remove a NuGet package
dotnet remove package Newtonsoft.Json

# List installed templates
dotnet new list

# Install a new template
dotnet new install Microsoft.AspNetCore.SpaTemplates::*

# Create a solution file
dotnet new sln -n MySolution

# Add a project to a solution
dotnet sln MySolution.sln add MyProject/MyProject.csproj

# Run tests
dotnet test

# Generate a new GUID
dotnet new guid
```

## Visual Studio Code Extensions

Visual Studio Code is a popular, lightweight code editor that can be enhanced with extensions for C# development.

1. **C# (by Microsoft)**: Essential extension for C# development.
   - Intellisense, debugging, refactoring, code navigation
   - Install: `ext install ms-dotnettools.csharp`

2. **C# Extensions (by JosKreativ)**: Provides additional C# features.
   - Create new C# classes and interfaces
   - Install: `ext install jchannon.csharpextensions`

3. **.NET Core Test Explorer**: Run and debug tests within VS Code.
   - Install: `ext install formulahendry.dotnet-test-explorer`

4. **NuGet Package Manager**: Manage NuGet packages directly from VS Code.
   - Install: `ext install jmrog.vscode-nuget-package-manager`

5. **REST Client**: Send HTTP requests and view responses directly in VS Code.
   - Install: `ext install humao.rest-client`

6. **GitLens**: Enhanced Git integration and exploration.
   - Install: `ext install eamodio.gitlens`

7. **Prettier - Code formatter**: Code formatting support (including C#).
   - Install: `ext install esbenp.prettier-vscode`

8. **Better Comments**: Improve code documentation with color-coded comments.
   - Install: `ext install aaron-bond.better-comments`

9. **vscode-icons**: File and folder icons for better visual organization.
   - Install: `ext install vscode-icons-team.vscode-icons`

10. **Code Spell Checker**: Spelling checker for source code.
    - Install: `ext install streetsidesoftware.code-spell-checker`

## NuGet Package Manager

NuGet is the package manager for .NET. Here are some common NuGet commands:

```bash
# Add a package to a project
dotnet add package PackageName

# Install packages listed in project file
dotnet restore

# Remove a package
dotnet remove package PackageName

# List installed packages
dotnet list package

# Update a package
dotnet add package PackageName --version VersionNumber

# Create a NuGet package
dotnet pack

# Publish a package to NuGet.org
dotnet nuget push PackageName.nupkg --api-key YourApiKey --source https://api.nuget.org/v3/index.json
```

## Project Templates

.NET provides various project templates. Here are some commonly used ones:

```bash
# Console Application
dotnet new console

# Class Library
dotnet new classlib

# ASP.NET Core Web App (Model-View-Controller)
dotnet new mvc

# ASP.NET Core Web API
dotnet new webapi

# Blazor WebAssembly App
dotnet new blazorwasm

# Blazor Server App
dotnet new blazorserver

# React.js with ASP.NET Core
dotnet new react

# Angular with ASP.NET Core
dotnet new angular

# Vue.js with ASP.NET Core
dotnet new vue

# xUnit Test Project
dotnet new xunit

# NUnit Test Project
dotnet new nunit
```

## Build Tools

### MSBuild
MSBuild is the build system for .NET and Visual Studio.

```bash
# Build a project or solution
msbuild MySolution.sln

# Build with a specific configuration
msbuild MySolution.sln /p:Configuration=Release

# Clean the build outputs
msbuild MySolution.sln /t:Clean

# Build and run tests
msbuild MySolution.sln /t:Build;Test
```

### CAKE (C# Make)
CAKE is a cross-platform build automation system with a C# DSL.

```csharp
// Example build.cake file
var target = Argument("target", "Default");

Task("Clean")
    .Does(() =>
{
    CleanDirectory("./build");
});

Task("Build")
    .IsDependentOn("Clean")
    .Does(() =>
{
    DotNetCoreBuild("./MySolution.sln", new DotNetCoreBuildSettings
    {
        Configuration = "Release"
    });
});

RunTarget(target);
```

## Testing Tools

### xUnit
```bash
# Run tests
dotnet test

# Run tests with filter
dotnet test --filter "FullyQualifiedName~TestNamespace.TestClass.TestMethod"

# Run tests and generate coverage report
dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=cobertura
```

### NUnit
```bash
# Run tests
dotnet test

# Run tests with specific trait
dotnet test --filter "TestCategory=UnitTest"

# Run tests and output results to file
dotnet test --logger:"trx;LogFileName=testresults.trx"
```

## Code Analysis Tools

### Roslyn Analyzers
Roslyn analyzers are included in the .NET SDK and can be configured in the project file.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
    <EnableNETAnalyzers>true</EnableNETAnalyzers>
    <AnalysisMode>AllEnabledByDefault</AnalysisMode>
  </PropertyGroup>
</Project>
```

### StyleCop Analyzers
StyleCop helps enforce consistent code style and formatting.

```bash
# Install StyleCop Analyzers
dotnet add package StyleCop.Analyzers
```

### SonarQube
SonarQube provides comprehensive code quality and security analysis.

```bash
# Install SonarScanner for .NET
dotnet tool install --global dotnet-sonarscanner

# Run SonarQube analysis
dotnet sonarscanner begin /k:"project-key"
dotnet build
dotnet sonarscanner end
```

## Debugging Tools

### Visual Studio Code Debugger
- Set breakpoints by clicking on the gutter (left side of line numbers)
- Use F5 to start debugging
- Use Shift+F5 to stop debugging
- Use F10 for step over, F11 for step into

### OmniSharp
OmniSharp provides a common platform for .NET development across editors and IDEs.

```json
// Example launch.json configuration
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": ".NET Core Launch (console)",
            "type": "coreclr",
            "request": "launch",
            "preLaunchTask": "build",
            "program": "${workspaceFolder}/bin/Debug/net6.0/MyApp.dll",
            "args": [],
            "cwd": "${workspaceFolder}",
            "console": "internalConsole",
            "stopAtEntry": false
        }
    ]
}
```

## Performance Profiling

### dotnet-trace
dotnet-trace is a cross-platform CLI tool for collecting .NET traces for performance analysis.

```bash
# Install dotnet-trace
dotnet tool install --global dotnet-trace

# Collect a trace
dotnet trace collect --process-id <PID>

# Analyze the trace
dotnet trace analyze <trace-file.nettrace>
```

### BenchmarkDotNet
BenchmarkDotNet is a powerful benchmarking library for .NET.

```csharp
using BenchmarkDotNet.Attributes;
using BenchmarkDotNet.Running;

public class MyBenchmarks
{
    [Benchmark]
    public void MyBenchmarkMethod()
    {
        // Code to benchmark
    }
}

class Program
{
    static void Main(string[] args)
    {
        var summary = BenchmarkRunner.Run<MyBenchmarks>();
    }
}
```

## Containerization and Deployment

### Docker
Docker can be used to containerize .NET applications.

```dockerfile
# Example Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MyApp.csproj", "./"]
RUN dotnet restore "MyApp.csproj"
COPY . .
RUN dotnet publish "MyApp.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "MyApp.dll"]
```

### Azure DevOps
Azure DevOps can be used for CI/CD pipelines.

```yaml
# Example azure-pipelines.yml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

variables:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  inputs:
    command: 'restore'
    projects: '**/*.csproj'

- task: DotNetCoreCLI@2
  inputs:
    command: 'build'
    projects: '**/*.csproj'
    arguments: '--configuration $(buildConfiguration)'

- task: DotNetCoreCLI@2
  inputs:
    command: 'test'
    projects: '**/*Tests/*.csproj'
    arguments: '--configuration $(buildConfiguration)'

- task: DotNetCoreCLI@2
  inputs:
    command: 'publish'
    publishWebProjects: true
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'

- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: '$(Build.ArtifactStagingDirectory)'
    artifactName: 'myWebsiteName'
```

This cheat sheet covers a wide range of tools and extensions useful for modern C# development, including CLI tools, VSCode extensions, build and test tools, code analysis, debugging, performance profiling, and deployment options. It should serve as a handy reference for developers working on C# projects.
