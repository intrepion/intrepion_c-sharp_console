# intrepion_c-sharp_console
intrepion C# console development files

# C# Console Project Template

This repository provides a template for creating C# console projects using .NET 8.0 in a Docker environment. The setup ensures consistent development environments across different machines and operating systems while supporting a flexible project organization structure.

## Project Layout

The template is organized into two main parts: the template files and your project files.

The template files are organized as follows:
```
template-root/
├── docker/
│   ├── Dockerfile       # Development environment setup
│   └── Dockerfile.new   # Project initialization environment
├── scripts/
│   └── new.sh           # Project creation script
└── docker-compose.yml   # Docker services configuration
```

When you create a new project, it generates a structure that mirrors GitHub's organization:
```
github/
├── [GITHUB_NAME]/
│   └── [REPO_NAME]/
│       └── [APP_NAME]/
│           ├── [APP_NAME].sln
│           ├── [APP_NAME].BusinessLogic/
│           │   └── [Library source files]
│           └── [APP_NAME].BusinessLogic.UnitTests/
│               └── [Test files]
```

For example, if you initialize a project with:
- GITHUB_NAME=intrepion
- REPO_NAME=my-project
- APP_NAME=Intrepion.MyProject

The resulting structure would be:
```
github/
├── intrepion/
│   └── my-project/
│       └── Intrepion.MyProject/
│           ├── Intrepion.MyProject.sln
│           ├── Intrepion.MyProject.BusinessLogic/
│           └── Intrepion.MyProject.BusinessLogic.UnitTests/
```

## Prerequisites

To use this template, you'll need:
- Docker Desktop (or Docker Engine and Docker Compose for Linux)
- Git for version control

A local .NET installation is not required since all .NET operations occur within Docker containers.

## Creating a New Project

The template uses environment variables to configure project creation. Here's how to initialize a new project:

```bash
APP_NAME=Intrepion.MyProject GITHUB_NAME=intrepion REPO_NAME=my-project docker compose run --rm c-sharp-new
```

This command performs several operations:
1. Creates a new solution file named after your APP_NAME
2. Sets up a class library project for your business logic
3. Creates a unit test project that references your business logic project
4. Configures all necessary project references and dependencies

## Development Workflow

After creating your project, you can perform various development tasks using the development container. Remember to provide the same environment variables used during initialization:

For testing your code:
```bash
APP_NAME=Intrepion.MyProject GITHUB_NAME=intrepion REPO_NAME=my-project docker compose run --rm c-sharp dotnet test
```

For building the solution:
```bash
APP_NAME=Intrepion.MyProject GITHUB_NAME=intrepion REPO_NAME=my-project docker compose run --rm c-sharp dotnet build
```

For restoring NuGet packages:
```bash
APP_NAME=Intrepion.MyProject GITHUB_NAME=intrepion REPO_NAME=my-project docker compose run --rm c-sharp dotnet restore
```

## Environment Variables

The template requires three environment variables for both initialization and development:

- APP_NAME: The full name of your application (e.g., Intrepion.MyProject)
  - This becomes the name of your solution and the base name for your projects
  - Should follow C# naming conventions (PascalCase)
  
- GITHUB_NAME: Your GitHub username or organization name
  - Used to create the correct directory structure
  - Ensures consistency with GitHub repository organization
  
- REPO_NAME: The name of your repository
  - Should match your GitHub repository name
  - Used for organizing projects under your GitHub account

## Docker Environments

The template provides two specialized Docker environments:

1. Development Environment (c-sharp):
   - Based on the .NET 8.0 SDK
   - Includes development tools like dotnet-format
   - Used for ongoing development tasks
   - Mounts your project directory for live editing

2. Initialization Environment (c-sharp-new):
   - Based on the .NET 8.0 SDK
   - Contains the project initialization script
   - Used only when creating new projects
   - Creates the initial project structure

## Troubleshooting Guide

If you encounter issues, follow these steps:

1. Environment Variable Problems:
   - Verify all three environment variables are set correctly
   - Check for typos in variable names and values
   - Ensure values follow naming conventions

2. Directory Issues:
   - Confirm the target directory doesn't already exist
   - Verify write permissions in the parent directory
   - Check the directory structure matches the template

3. Docker Problems:
   - Ensure Docker is running
   - Check Docker logs for detailed error messages
   - Verify Docker Compose is installed and working

4. Build or Runtime Issues:
   - Review Docker build logs for errors
   - Check the .NET SDK version in containers
   - Verify project file syntax and references

## Contributing

When contributing to this template:

1. Test the initialization process with:
   - Different project names and structures
   - Various operating systems
   - Different user permissions

2. Verify functionality:
   - Test all development commands
   - Ensure cross-platform compatibility
   - Check Docker configuration portability

3. Document changes:
   - Update README with new features
   - Document any breaking changes
   - Provide migration guides if needed

## Support

If you need help:
1. Check the troubleshooting guide above
2. Verify your environment setup
3. Open an issue in the GitHub repository with:
   - Your environment details
   - Steps to reproduce the problem
   - Error messages and logs
   - What you've tried so far
