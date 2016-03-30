##### Error Reports

In general, WorkstationClient is designed not to emit any exceptions for security reasons.
However when a severe or unhandled error occurs at the client's side, a report is generated to help troubleshooting.

The filepath can be found at the 'ErrorReport' property of the returned **_ClientError_**.
By design, each report is automatically saved inside the local computer's Temp folder, as you can see below.

![alt text](https://github.com/vkokkinid/WorkstationClient.1.2.0/blob/master/generated_error_reports.jpg "Error reports at the local Temp folder")

The particular file contains information about the internal function that failed (similar to a Windows crash dump), is encrypted and thus unreadable to anyone but Plexscape.
It's up to you to decide how generated reports will be collected from the customer's computer and forwarded to Plexscape.

Please take a look at *ConsoleDisplay.cs* in the provided samples for a very simple integration of the discussed feature.

You can invoke it if you "force" a network connection loss, either before or while running the client, and then call one of its methods to get the error result.

Possible ways to simulate offline state:
- Pull the ethernet cable plug for desktop PCs.
- Stop WiFi connection for laptops.
- Disable the network adapter of your computer etc.

