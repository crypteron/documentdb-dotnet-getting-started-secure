# Crypteron + DocumentDB = rapid development of highly secure cloud apps

This is a quick demo showing how to use Crypteron CipherObject to secure data in DocumentDB. Enabling pervasive encryption with just a couple of lines of code, Crypteron’s Security Framework transparently handles all aspects of privacy, tamper protection, secure key distribution, secure key storage, access controls, audit logs, key revocations, key rotations and more. The NuGet package is Crypteron.CipherObject

Observe the `GeneticCondition` field when you run this sample app. Before deleting the database at the end, compare the console output with the at-rest storage data (e.g. via portal.azure.com => DocumentDB => Document Explorer). Other than your own code, everyone else only sees strongly encrypted data.

## Current limitations

NOTE: Commercial customers can contact us at support(at)crypteron.com to request and sponsor features

### Only top level fields and properties are secured 

If you have `thisObject.SSN`, Crypteron.CipherObject.Seal(thisObject) will suffice. But if you have `thisObject.Child.SSN` it won't. You can however use `Crypteron.CipherObject.Seal(thisObject.Child)` instead. 

### `JObject` type is not supported

If writing objects of type `T` (which contains `Secure` properties), when reading them back they should also be of the same type `T`. Return type of `JObject` is currently not supported for decryption of secured values. This means instead of `client.CreateDocumentQuery(...)` one should use something like `client.CreateDocumentQuery<Family>(...)` before `Unseal`ing the result objects.

----

## Original README.md below

---
services: documentdb
platforms: dotnet
author: andrewhoh
---

# Developing a .NET console app using DocumentDB
This sample shows you how to use the Microsoft Azure DocumentDB service to store and access data from a .NET console application.

![.NET Console application](./media/image1.png)

For a complete end-to-end walkthrough of creating this application, please refer to the [full tutorial on the Azure documentation page](https://azure.microsoft.com/documentation/articles/documentdb-get-started/).

## Running this sample

1. Before you can run this sample, you must have the following perquisites:
	- An active Azure DocumentDB account - If you don't have an account, refer to the [Create a DocumentDB account](https://azure.microsoft.com/en-us/documentation/articles/documentdb-create-account/) article.
	- Visual Studio 2013 (or higher).

2.Clone this repository using Git for Windows (http://www.git-scm.com/), or download the zip file.

3.From Visual Studio, open the **GetStarted.sln** file from the root directory.

4.In Visual Studio Build menu, select **Build Solution** (or Press F6). 

5.Retrieve the URI and PRIMARY KEY (or SECONDARY KEY) values from the Keys blade of your DocumentDB account in the Azure Preview portal. For more information on obtaining endpoint & keys for your DocumentDB account refer to [How to manage a DocumentDB account](https://azure.microsoft.com/en-us/documentation/articles/documentdb-manage-account/#keys)

If you don't have an account, see [Create a DocumentDB database account](https://azure.microsoft.com/en-us/documentation/articles/documentdb-create-account/) to set one up.

6.In the **App.config** file, located in the src directory, find **endpoint** and **authKey** and replace the placeholder values with the values obtained for your account.

    <add key="EndPointUrl" value="~your DocumentDB endpoint here~" />
    <add key="AuthorizationKey" value="~your auth key here~" />

7.You can now run and debug the application locally by pressing **F5** in Visual Studio.

## About the code
The code included in this sample is intended to get you quickly started with a .NET console application that connects to Azure DocumentDB.

## More information

- [Azure DocumentDB Documentation](https://azure.microsoft.com/en-us/documentation/services/documentdb/)
- [Azure DocumentDB .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)
- [Azure DocumentDB .NET SDK Reference Documentation](https://msdn.microsoft.com/library/azure/dn948556.aspx)
