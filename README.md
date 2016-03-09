### WorkstationClient.1.2.0
Repo for clients of version 1.2.0 (2016-02-26).
New generation client that is **not compatible** with previous versions (1.0.1 and older).
Supports file API, error reports and offline mode, as well as asynchronous requests for net45 builds.

##### List of Changes
- Constants residing in *PlexResponseCode* have been removed. You must declare own class containing the code(s) that your application uses. Please check *ResponseCode.cs* in the provided samples for a full listing of the available status codes.
- *InitWorkstation()* method has been renamed to **_StartSession()_**. You must explicitly call **_EndSesion()_**, the former  *UnloadClient()*, when the client is no longer needed.
- *PlexDtoKeys* class has been renamed to **_DtoKeys_**.
- The majority of calls to WorkstationClient now return some type of **_ClientResult_** object. This particular object contains
  - either the value of the result (or null for *void* methods) when successful
  - or a **_ClientError_** when an error occurs.
- **_ClientError_** has replaced *PlexError*, i.e. carries the status code and message. Additionally, it can contain the path of a generated error report, when a client-side exception happens. Note that WorkstationClient is designed not to emit any exceptions for security reasons. The caller must check the failed result and decide whether to handle any generated error report(s) - see the provided implementation in *ConsoleDisplay.cs* for an idea of how it can be used.
- New method **_GetClientInfo()_** returns useful client information. Depending on the overall workstation/subscription state, values are returned for 'DtoKeys.StationReference', 'DtoKeys.CallerIp', 'DtoKeys.SubReference', 'DtoKeys.SubName' etc. This method doesn't return errors and should be used to display information needed for troubleshooting.
- New **_File API_** feature, that gives the ability to store and synchronize configured files between clients. Check the proposed implementation for details.
