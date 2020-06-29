Resource: https://docs.microsoft.com/en-us/aspnet/core/tutorials/grpc/grpc-start?view=aspnetcore-3.1&tabs=visual-studio-code



Create new project 

```bash
cd dotnet-service
dotnet new grpc
dotnet dev-certs https --trust

dotnet run
```



issues on macos : https://docs.microsoft.com/en-us/aspnet/core/grpc/troubleshoot?view=aspnetcore-3.1#unable-to-start-aspnet-core-grpc-app-on-macos

- Configure Kestrel to not use TLS for on server side
- For the client also we will need to disable TLS.

```
The gRPC template is configured to use Transport Layer Security (TLS). gRPC clients need to use HTTPS to call the server.

macOS doesn't support ASP.NET Core gRPC with TLS. Additional configuration is required to successfully run gRPC services on macOS. For more information, see Unable to start ASP.NET Core gRPC app on macOS.
```

- Change the `Program.cs` as

  ```
  Host.CreateDefaultBuilder(args)
          .ConfigureWebHostDefaults(webBuilder =>
          {
              webBuilder.ConfigureKestrel(options =>
              {
                  // Setup a HTTP/2 endpoint without TLS.
                  options.ListenLocalhost(5000, o => o.Protocols = 
                      HttpProtocols.Http2);
              });
              webBuilder.UseStartup<Startup>();
          });
  ```

  

- now restart the project using `dotnet run`



### Testing gRPC service 

- launch app [BoolRPC](https://github.com/uw-labs/bloomrpc)

- import the .proto folder from the project

- play the Greeter request : 

  ![image-20200629211401480](/Users/dawn/Documents/projects/grpc-stub/dotnet-service/docs/images/bloomrpc-greeter.png)





### Creating a client with .NET

- Create a console app with .NET

  ```bash
  # Create project
  mkdir dotnet-client
  cd dotnet-client
  dotnet new console
  
  # Add required Nugets
  dotnet add dotnet-client.csproj package Grpc.Net.Client
  dotnet add dotnet-client.csproj package Google.Protobuf
  dotnet add dotnet-client.csproj package Grpc.Tools
  ```

  

- Add nuggets