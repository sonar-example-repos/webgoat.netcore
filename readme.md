# dotTEST WebGoat.NET Example

This example shows the following dotTEST capabilities:

- Static analysis and flow analysis capabilities
- Integration with GitHub pipelines via the [Run dotTEST Action](https://github.com/parasoft/run-dottest-action)
- Integration with Aider to apply static analysis fixes in GitHub pipelines (dotTEST Autofix feature)

## Table of Contents

- [dotTEST capabilities](#dotTEST-capabilities)
- [About WebGoat.NET project](#WebGoatNET-version-03)

## dotTEST Capabilities

### Static Analysis

Static analysis and flow analysis help you verify code quality and ensure compliance with industry standards, such as CWE or OWASP. Static analysis is a software testing method that examines the source code without executing it to detect errors, vulnerabilities, and violations of coding standards. Flow analysis refers to the examination and evaluation of data or control flow within a program or system to identify potential issues such as resource leaks, dead code, security vulnerabilities, or performance bottlenecks. 
See [Parasoft dotTEST User Guide](https://docs.parasoft.com/display/DOTTEST20252) for details regarding static and flow analysis with dotTEST as well as other dotTEST capabilities.

### Run Parasoft dotTEST GitHub Action

The `Run Parasoft dotTEST` action enables you to run code analysis with dotTEST and review analysis results directly on GitHub. To launch code analysis with dotTEST, add the `Run Parasoft dotTEST` action to your GitHub workflow. [The example](https://github.com/parasoft/run-dottest-action/blob/master/samples/run-dottest-analyzer-template.yml) illustrates a simple workflow consisting of one job "run-dottest-action".

See [Run dotTEST Action @ GitHub Marketplace](https://github.com/marketplace/actions/run-parasoft-dottest) for details regarding configuration and usage.
See also [Run dotTEST Action project](https://github.com/parasoft/run-dottest-action).


### Autofix in CI/CD Using Aider

`DottestAutoFix` is a Python-based script that leverages AI-powered code analysis to automatically fix dotTEST violations in your .NET projects, based on a generated analysis report. Once a fix is applied, the plugin validates it using `dottestcli` and then adds a commit to the current branch in your project repository.
The following example shows a simple Autofix execution:
```batch
@REM Execute autofix with recommended settings
python DottestAutoFix.py ^
 --report ".dottest/report/report.xml" ^
 --max-attempts 3 ^
 --solution BankExample.sln ^
 --tool-home "C:\Program Files\Parasoft\dotTEST\2025.2"
```

See [**LINK**](https://docs.parasoft.com/display/DOTTEST20252/Fixing+Violations+Using+Autofix) for details regarding Autofix configuration and usage.
TODO: Add link to official documentation describing this feature

## WebGoat.NET version 0.3

### Build Status

![build .NET 8](https://github.com/tobyash86/WebGoat.NET/workflows/build%20.NET%208/badge.svg)

### The Next-Generation WebGoat Example Project Demonstrating OWASP Top 10 Vulnerabilities

This is a re-implementation of the original [WebGoat project for .NET](https://github.com/rappayne/WebGoat.NET).

This web application is a learning platform that attempts to explain 
common web security flaws. It contains generic security flaws that apply to
most web applications. It also includes lessons that specifically pertain to
the .NET framework. The exercises in this app are intended to demonstrate 
web security attacks and show how developers can overcome them.

#### WARNING!: 
THIS WEB APPLICATION CONTAINS NUMEROUS SECURITY VULNERABILITIES 
WHICH WILL RENDER YOUR COMPUTER VERY INSECURE WHILE RUNNING. IT IS HIGHLY
RECOMMENDED TO COMPLETELY DISCONNECT YOUR COMPUTER FROM ALL NETWORKS DURING USE.

#### Notes:
 - Google Chrome performs filtering for reflected XSS attacks. These attacks
   will not execute unless Chrome is run with the argument 
   `--disable-xss-auditor`.

### Requirements
- .NET 8 SDK

### Building and Running the WebGoat.NET Example

#### 1. Running the Example in a Docker Container

The provided Dockerfile is compatible with both Linux and Windows containers.  
To build a Docker image, execute the following command:

```sh
docker build --pull --rm -t webgoat.net .
```

Please note that the Linux image is already built by the pipeline and can be pulled from [here](https://github.com/users/tobyash86/packages?repo_name=WebGoat.NET).

##### Linux Containers

To run the `webgoat.net` image, execute the following command:

```sh
docker run --rm -d -p 5000:80 --name webgoat.net webgoat.net
```

The WebGoat.NET website should be accessible at http://localhost:5000.

##### Windows Containers

To run the `webgoat.net` image, execute the following command:

```sh
docker run --rm --name webgoat.net webgoat.net
```

Windows containers do not support binding to localhost. To access the website, you need to provide the IP address of your Docker container. To obtain the IP, execute the following command:

```sh
docker exec webgoat.net ipconfig
```
The output will include the IP of the 'webgoat.net' container, for example:

```
Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::1967:6598:124:cfa3%4
   IPv4 Address. . . . . . . . . . . : 172.29.245.43
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Default Gateway . . . . . . . . . : 172.29.240.1
```

In the above example, you can access the WebGoat.NETCore website at http://172.29.245.43.

##### Stopping the Docker Container

To stop the `webgoat.net` container, execute the following command:

```sh
docker stop webgoat.net
```

#### 2. Running the Example Locally Using dotnet.exe (Kestrel)

1. Build and publish WebGoat.NET using the following command:

```sh
dotnet publish -c release -o ./app 
```

The web application will be deployed to the `app` folder in the current directory.

2. Execute the web application on localhost using the following command:

```sh
dotnet ./app/WebGoat.NET.dll --urls=http://localhost:5000
```

The WebGoat.NET website will be accessible at the URL specified with the `--urls` parameter: http://localhost:5000.

#### 3. Running the Example Using a Script
The WebGoat.NET project ships with scripts that allow you to conveniently run the web application. The following scripts are located in the `script` directory at the root of the project:
- runInDocker.bat - runs the application in a Docker container on Windows.
- runInDocker.sh - runs the application in a Docker container on Linux.
- runLocal.bat - runs the application locally on Windows.
- runLocal.sh - runs the application locally on Linux.

### Known Issues:

1. The latest OWASP Top 10 is not covered. The missing vulnerabilities need to be added to the codebase.
2. Educational documents and training materials for any categories of the latest OWASP Top 10 are not available.










