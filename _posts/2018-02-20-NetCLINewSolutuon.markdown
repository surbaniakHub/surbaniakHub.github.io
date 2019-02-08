---
layout: post
title:  "New solution witch .Net Core CLI"
date:   2018-02-20 21:42:46 +0000
categories: .NET Core
tags: [.NET Core, CLI]
---
**This tutorial presents how to create the new solution using .NET Core CLI.**

This tutorial requires:

  1. Visual Studio Code with extension C#.
  2. .NET CORE 2.*.

# Step 1

In the solution directory, create two additional directories using command prompt eg.:

```bash
> mkdir src
> mkdir tests
```

In the “src” directory, create three projects eg.”AdsApp.Core, AdsApp.Infrastructure and AdsApp.Web” using the commands:

```bash
> dotnet new classlib -n AdsApp.Core
> dotnet new classlib -n AdsApp.Infrastructure
> dotnet new mvc -n AdsApp.Web
```

Navigate to the “tests” directory, create one project “AdsApp.uTest” by the command:

```bash
> dotnet new xunit -n AdsApp.uTest
```

go back to the main solution directory and add the solution file by the command:

```bash
> dotnet new sln -n AdsApp
```

# Step 2

Next, add projects to solution using the commands:

```bash
> dotnet sln AdsApp.sln add src\AdsApp.Core\AdsApp.Core.csproj
> dotnet sln AdsApp.sln add src\AdsApp.Infrastructure\AdsApp.Infrastructure.csproj
> dotnet sln AdsApp.sln add src\AdsApp.Web\AdsApp.Web.csproj
> dotnet sln AdsApp.sln add tests\AdsApp.uTest\AdsApp.uTest.csproj
```

This is the structure of directories:

```bash
C:.
├───src
│   ├───AdsApp.Core
│   │   ├───bin
│   │   │   └───Debug
│   │   │       └───netstandard2.0
│   │   └───obj
│   │       └───Debug
│   │           └───netstandard2.0
│   ├───AdsApp.Infrastructure
│   │   ├───bin
│   │   │   └───Debug
│   │   │       └───netstandard2.0
│   │   └───obj
│   │       └───Debug
│   │           └───netstandard2.0
│   └───AdsApp.Web
│       ├───bin
│       │   └───Debug
│       │       └───netcoreapp2.0
│       ├───Controllers
│       ├───Models
│       ├───obj
│       │   └───Debug
│       │       └───netcoreapp2.0
│       ├───Views
│       │   ├───Home
│       │   └───Shared
│       └───wwwroot
│           ├───css
│           ├───images
│           ├───js
│           └───lib
│               ├───bootstrap
│               │   └───dist
│               │       ├───css
│               │       ├───fonts
│               │       └───js
│               ├───jquery
│               │   └───dist
│               ├───jquery-validation
│               │   └───dist
│               └───jquery-validation-unobtrusive
└───tests
    └───AdsApp.uTest
        ├───bin
        │   └───Debug
        │       └───netcoreapp2.0
        └───obj
            └───Debug
                └───netcoreapp2.0
```

# Step 3

Add relationships between projects and also properties “AssemblyName”:
In the file “AdsApp.Infrastructure.csproj”

```csharp
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AssemblyName>AdsApp.Infrastructure</AssemblyName>
    <PackageId>AdsApp.Infrastructure</PackageId>
  </PropertyGroup>
  <ItemGroup>
  <ProjectReference Include="../AdsApp.Core/AdsApp.Core.csproj"/>
  </ItemGroup>
</Project>
```

In the file “AdsApp.Web.csproj”

```csharp
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
    <AssemblyName>AdsApp.Web</AssemblyName>
    <PackageId>AdsApp.Web</PackageId>
  </PropertyGroup>
  <ItemGroup>
    <ProjectReference Include="../AdsApp.Infrastructure/AdsApp.Infrastructure.csproj" />
  </ItemGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
  </ItemGroup>
  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
  </ItemGroup>
</Project>
```

In the file “AdsApp.Core.csproj”

```csharp
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AssemblyName>AdsApp.Core</AssemblyName>
    <PackageId>AdsApp.Core</PackageId>
  </PropertyGroup>
</Project>
```

# Step 4

In the main directory of solution, we call commands:

```bash
> dotnet restore
> dotnet build
```

This episode shows how to create a basic solution without MS Visual Studio IDE. Of course, this is not the simplest method, but it allows us to get to know the structure of dependencies in the project.