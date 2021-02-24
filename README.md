# azure-functions-dotnet5-examples
This is my personal playground for discovering the .NET 5 Azure functions worker preview, it might turn into a blog later.

If you are confused, you can read some background here [.NET 5 support on Azure Functions](https://techcommunity.microsoft.com/t5/apps-on-azure/net-5-support-on-azure-functions/ba-p/1973055)

> Everything here is based on https://github.com/Azure/azure-functions-dotnet-worker-preview

## Nice to know

### Why is there a TimerInfo record?
The timer function depends on the included TimerInfo class, for now it does not work with the normal Microsoft.Azure.WebJobs.TimerInfo
the TimerInfo class is implemented as a record to keep it clean ;)

### Dependency injection in Startup?
If you were used to the Azure Functions Startup class, it is not here. It is actually now using a HostBuilder that you can find in Program.cs

### No ILogger method injection?
Nope, instead you can get FunctionExecutionContext which has the Logger and other goodies.

### How to run:
- Install .NET 5.0
- Get core tools >= 3.0.3160: https://github.com/Azure/azure-functions-core-tools
- Open the project in Visual Studio or VsCode.
- Open a terminal: 
``` 
cd ExampleFunction
func host start --verbose
The debugger will try to attach to your vs instance.
```

> Since preview4 the example was crashing on the UseDevelopmentStorage=true
> It looks like only azurite (new storage emulator) is supported for now (or it's me)

### How to run Azurite
```
# if you run docker:
docker run -p 10000:10000 -p 10001:10001 mcr.microsoft.com/azure-storage/azurite

# or install it from npm and run it
npm install -g azurite
mkdir c:\azurite
azurite -s -l c:\azurite -d c:\azurite\debug.log
```


### How to run in a devcontainer:

- Open vscode
- Install the `Remote - Container` extension
- Re-open the directory in a container `Remote - Containers: Open folder in Container`

Now you can execute the same commands as in How to run
