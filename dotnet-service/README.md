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



