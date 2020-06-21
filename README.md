# svcutil-playground
Quick example project to play with Svcutil.exe.

This project requires that the Windows Communication Foundation components have been installed in Visual Studio. This is not always the default, so it might require special attention.

Compile the project to generate the following files:
- WcfServiceLibrary.dll - generated code
- WcfServiceLibrary.dll.config - configuration for the WCF service
- WcfServiceLibrary.pdb - debug information for the dll

To verify the service configuration, run the following command:
```bash
svcutil /validate /serviceName:WcfServiceLibrary.Service1 WcfServiceLibrary.dll
```

To generate WSDL/XSD files, run the following command:
```bash
svcutil WcfServiceLibrary.dll
```
This will generate the following files:
- tempuri.org.wsdl - service definition
- tempuri.org.xsd - schema that defines request and response types
- schemas.microsoft.com.2003.10.Serialization.xsd - base schema that defines primitives
- WcfServiceLibrary.xsd - schema that defines complex data types from data contracts, etc.

To generate the proxy class for the client, run the following command:
```bash
svcutil tempuri.org.wsdl *.xsd
```
This will generate the following files
- schemas.microsoft.com.2003.10.Serialization.cs - code for a client to call a Service1 instance
- output.config - configuration for the WCF client

> Note: XSD files are required in addition to the WSDL file when running svcutil against local files. If svcutil is run against a live service url, then this information should be available from the live service.
