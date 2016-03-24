##### File API

Some details about how to monitor and sync an application file between workstations of the same subscription.

A file descriptor, named the file tag, must be configured via the management console.
We already provided a tag, '*SettingsForAccount*', which is primarily intended for application settings/configutation etc.
Note that the contents, format or even the desired "logic" of the actual file is arbitrary and the licensing system's behaviour 
is not affected by it, by any means.

![alt text](https://github.com/vkokkinid/WorkstationClient.1.2.0/blob/master/console_monitored_file_tag.JPG "A file tag")

Using this file descriptor a workstation has the ability to:

1. Create the first instance of the monitored file - **_CreateFile_**.

2. Check to see if a newer version exists - **_HasNewerFileVersion_**.

3. Retrieve the latest version - **_GetFile_**.

4. Set the latest version with new content - **_UpdateSynchronizedFile_**.

5. View history of changes - **_GetFileHistory_**.

Those functions are the bare bones of a version control system.

A client application could call *CreateFile* **(1)** upon succesful activation of the subscription.
Alternatively you could use the the management console to upload the file, either manually or automatically (feature open to discussion).
The moment a version of the file exists, all workstations under the particular subscription can access it using the API.

The simplest synchronization method is to periodically call *HasNewerFileVersion* **(2)** and if a newer version exists,
call *GetFile* **(3)** to download the actual file.
Note that any comparisons, validations and integrity checks regarding the content are responsibility of the caller application.
Effectively, the File API just passes around chuncks of binary data.

If the workstation wants to modify the file contents, *UpdateSynchronizedFile* **(4)** must be called.
If someone else has uploaded another version in the meantime, an error is emitted so that the caller
can decide whether to synchronize again or force an overwrite by setting the optional parameter '*forceUpdate*' to true.

*GetFileHistory* **(5)** is a helper function mostly useful for debugging or reporting purposes.

Please study the provided samples for a demo implementation of the above functions.
