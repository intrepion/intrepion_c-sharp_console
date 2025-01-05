# /docker/Dockerfile

FROM mcr.microsoft.com/dotnet/sdk:8.0

WORKDIR /app

# Install required .NET tools
RUN dotnet tool install --global dotnet-format

# Add .NET tools to PATH
ENV PATH="${PATH}:/root/.dotnet/tools"
