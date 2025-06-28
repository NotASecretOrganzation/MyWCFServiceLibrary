# MyWCFServiceLibrary

A complete WCF (Windows Communication Foundation) service implementation demonstrating a calculator service with basic arithmetic operations.

## Overview

This project consists of three main components:

- **WcfServiceLibrary**: The core service library containing the calculator service implementation
- **WcfServiceHost**: A console application that hosts the WCF service
- **WcfServiceClient**: A console client application that consumes the service

## Features

The Calculator service provides the following operations:

- **Add**: Addition of two numbers
- **Subtract**: Subtraction of two numbers
- **Multiply**: Multiplication of two numbers
- **Divide**: Division of two numbers

## Project Structure

```text
MyWCFServiceLibrary/
├── ICalculator.cs              # Service contract interface
├── CalculatorService.cs        # Service implementation
├── WcfServiceLibrary.csproj    # Service library project
├── WcfServiceHost/             # Service hosting application
│   ├── Program.cs              # Host console application
│   └── App.config              # Host configuration
├── WcfServiceClient/           # Client application
│   ├── Program.cs              # Client console application
│   ├── App.config              # Client configuration
│   └── Connected Services/     # Generated service reference
└── README.md                   # This file
```

## Getting Started

### Prerequisites

- .NET Framework 4.x or later
- Visual Studio 2017 or later (recommended)
- Windows OS

### Building the Solution

1. Open the solution file `WcfServiceLibrary.sln` in Visual Studio
2. Build the entire solution (Build → Build Solution or Ctrl+Shift+B)

### Running the Service

1. **Start the Service Host:**
   - Set `WcfServiceHost` as the startup project
   - Run the application (F5 or Ctrl+F5)
   - The service will start on `http://localhost:8000/WcfService/`
   - You should see "The service is ready." message

2. **Run the Client:**
   - With the service host running, start the client
   - Set `WcfServiceClient` as the startup project and run it
   - The client will connect to the service and perform sample calculations

### Alternative: Run from Command Line

1. **Build the solution:**

   ```cmd
   msbuild WcfServiceLibrary.sln /p:Configuration=Debug
   ```

2. **Start the service host:**

   ```cmd
   cd WcfServiceHost\bin\Debug
   WcfServiceHost.exe
   ```

3. **Run the client (in a new terminal):**

   ```cmd
   cd WcfServiceClient\bin\Debug
   WcfServiceClient.exe
   ```

## Service Configuration

The service is configured to:

- Listen on `http://localhost:8000/WcfService/CalculatorService`
- Use WSHttpBinding for secure, reliable messaging
- Enable metadata exchange for service discovery
- Provide console logging of all operations

## Sample Usage

When running the client, you'll see output like:

```text
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
```

## Service Contract

The service implements the `ICalculator` interface:

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    
    [OperationContract]
    double Subtract(double n1, double n2);
    
    [OperationContract]
    double Multiply(double n1, double n2);
    
    [OperationContract]
    double Divide(double n1, double n2);
}
```

## Troubleshooting

### Common Issues

1. **Port already in use**: If port 8000 is occupied, modify the base address in `WcfServiceHost/Program.cs`
2. **Service not accessible**: Ensure Windows Firewall allows the application
3. **Build errors**: Verify all project references are correctly configured

### Service Discovery

You can view the service metadata by navigating to:
`http://localhost:8000/WcfService/?wsdl`

## Development Notes

- The service implementation includes console logging for all operations
- Error handling is implemented for communication exceptions
- The client uses a generated service reference for type-safe service consumption

## License

This project is provided as a sample/educational implementation of WCF services.