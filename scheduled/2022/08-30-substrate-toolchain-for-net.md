# Introduction to Substrate NET Toolchain/SDK and Unity integration

The [Substrate Toolchain for NET](https://github.com/ajuna-network/Ajuna.SDK) generates a full-fledged ready-to-hack Substrate SDK from any Substrate node compatible with metadata V14.
This toolchain is usable for any NET Applications and/or Unity.

The goal of this seminar is to show developers how to use a NET SDK (NET Standard 2.0 for maximum compatibility with Unity) to build applications from the metadata of any Substrate node.

**📆 Join the Crowdcast:** https://www.crowdcast.io/e/substrate-seminar-2/23

This seminar will be useful for developers who want to learn how to use the toolchain, specifically:

- C# developers
- Game developers trying to use leading game engines Unity or Unreal (UnrealCLR) with Substrate

## Outline

* Usage of the SDK
* Showcase exisiting projects
* Build a working Unity app
* Get in involved

## Learn more

[Ajuna.NetApi](https://github.com/ajuna-network/Ajuna.NetApi/tree/master/Ajuna.NetApi), is the basic framework for accessing and handling JSON-RPC connections and handling the generic RPC calls that every substrate node offer and are exposed by the rpc.methods(). It additionally implements rust primitives and generics as a C# representation like [U8](https://github.com/ajuna-network/Ajuna.NetApi/blob/master/Ajuna.NetApi/Model/Types/Primitive/U8.cs), [BaseVec](https://github.com/ajuna-network/Ajuna.NetApi/blob/master/Ajuna.NetApi/Model/Types/Base/BaseVec.cs) (Vec<>), or [EnumExt](https://github.com/ajuna-network/Ajuna.NetApi/blob/master/Ajuna.NetApi/Model/Types/Base/BaseEnumExt.cs) (Rust-specific Enums). The [Ajuna.NetApi](https://github.com/ajuna-network/Ajuna.NetApi/tree/master/Ajuna.NetApi) has no other types than the ones previously described, so accessing the node storage or sending extrinsic would involve manually creating the necessary types.

[Ajuna.NetApiExt](https://github.com/ajuna-network/SubstrateNET/tree/master/SubstrateNET.NetApi) is the extension of the NetApi, with a generated client extension, adding all the node-specific types, storage access, extrinsic calls and more to the client. As an example, here is the [FrameSystem](https://github.com/ajuna-network/SubstrateNET/blob/master/SubstrateNET.NetApi/Generated/Model/FrameSystem/MainSystem.cs). With the API and the Extensions, all possible interactions with a node and the specific network are given. However, if your application is targeted to be used by many consumers and needs to be on high availability to provide storage access or storage subscription, then accessing or subscribing straight to a node might be an issue in terms of scalability, but also in terms of efficiency.

[Ajuna.RestService](https://github.com/ajuna-network/SubstrateNET/tree/master/SubstrateNET.RestService), this service, in its core, just connects to a node and subscribes to the global storage changes, which are then maintained in memory. It holds all stored items exposed from a node and maintains them, and builds a swagger endpoint. On top, there is a REST service (poll) exposing all the storage information as REST, and additionally, there is a subscription service (pub/sub) providing changes over a WebSocket. This artifact is much more lightweight than the node and can be scaled according to the needs of the consumers without putting any load on an RPC node except for one connection for the global storage subscription.

![image](https://user-images.githubusercontent.com/17710198/182559250-76bc7f11-6aaf-473d-a72e-f9a6e964d073.png)

[Ajuna.RestClient](https://github.com/ajuna-network/SubstrateNET/tree/master/SubstrateNET.RestClient) is the artifact used in the client application C#, Unity, or whatever is using the client to access the information. It is the counterpart for the previously described service, allowing you to [subscribe](https://github.com/ajuna-network/SubstrateNET/blob/d42d23fa2f9bbd940df6b796ab1bd55a944b77fa/SubstrateNET.RestClient.Test/Generated/SystemControllerClientTest.cs#L109) to storage through the WebSocket or access storage through REST and providing it in an intuitive C# manner, where you can build events on storage changes and access REST by using the prepared node specific library. As an example, here is the pre-generated access for an account subscription (subscribe, [await](https://github.com/ajuna-network/SubstrateNET/blob/d42d23fa2f9bbd940df6b796ab1bd55a944b77fa/SubstrateNET.RestClient.Test/Generated/SystemControllerClientTest.cs#L117)) or getting the account through rest ([polling](https://github.com/ajuna-network/SubstrateNET/blob/d42d23fa2f9bbd940df6b796ab1bd55a944b77fa/SubstrateNET.RestClient.Test/Generated/SystemControllerClientTest.cs#L119)). This allows once you build your node specific SDK. You launched your Service to create Applications on top of the substrate without any further knowledge except the library usage.

![image](https://user-images.githubusercontent.com/17710198/182559346-592ab2b5-8047-4777-bd6c-ba100c971404.png)

## Resources

Here are some projects developed by Ajuna:

| Project | Description                                                                                                                                                                                                                                                                               | NuGet 
|---|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
| Ajuna.NetApi | Ajuna .NET API Full-featured substrate node API.                                                                                                                                                                                          | [![Nuget](https://img.shields.io/nuget/v/Ajuna.NetApi)](https://www.nuget.org/packages/Ajuna.NetApi/) |
| Ajuna.ServiceLayer | Implements the fundamental layer to access substrate node storage changes with a convenient API.                                                                                                                                                                                          | [![Nuget](https://img.shields.io/nuget/v/Ajuna.ServiceLayer)](https://www.nuget.org/packages/Ajuna.ServiceLayer/) |
| Ajuna.ServiceLayer.Model | Implements standard classes to easily share types between services and clients.                                                                                                                                                                                                           | [![Nuget](https://img.shields.io/nuget/v/Ajuna.ServiceLayer.Model)](https://www.nuget.org/packages/Ajuna.ServiceLayer.Model/) |
| Ajuna.AspNetCore | Implements extensions to the service layer that allow for quickly building a RESTful service to access your substrate node storage.                                                                                                                                                       | [![Nuget](https://img.shields.io/nuget/v/Ajuna.AspNetCore)](https://www.nuget.org/packages/Ajuna.AspNetCore/) |
| Ajuna.DotNet, Ajuna.DotNet.Template | .NET developer toolchain to scaffold actual projects such as a RESTful service including all the storage classes, types, and consumer clients. The projects generated with the generator toolchain are intended to be used for scaffolding and starting a substrate node service quickly. | [![Nuget](https://img.shields.io/nuget/v/Ajuna.DotNet)](https://www.nuget.org/packages/Ajuna.DotNet/) [![Nuget](https://img.shields.io/nuget/v/Ajuna.DotNet.Template)](https://www.nuget.org/packages/Ajuna.DotNet.Template/)|


 
