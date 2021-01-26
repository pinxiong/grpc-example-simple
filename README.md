## How gRPC works

This example will help you under gRPC better.

### Server

+ ServerBuilder: Create a `Server` instance, which will call `ServerProvider` directly.

+ ServerProvider: Create a `NettyServerProvider` as default, which will call `ServerRegistry`.

+ ServerRegistry: Create a `ServerRegistry` instance using `ServerRegistry#getDefaultRegistry()` and `ServerRegistry` will add all available `ServerProvider` instances by calling `ServiceProviders#loadAll(Class<T>, Iterable<Class<?>>, ClassLoader, PriorityAccessor<T>)`

+ ServiceProviders: Call `ServiceLoader#load(Class<T>, ClassLoader)` to create `NettyServerProvider` using SPI(`grpc-netty-shaded-1.35.0.jar!/META-INF/services/io.grpc.ManagedChannelProvider`) and Reflection

+ NettyServer: `ServerBuilder#start()` will call `NettyServer#start()` to let server work well


### Client

+ ManagedChannelProvider: create a `NettyChannelProvider` instance by using  SPI(`grpc-netty-shaded-1.35.0.jar!/META-INF/services/io.grpc.ManagedChannelProvider`) and Reflection

+ NettyChannelBuilder: create a channel that will connect with `NettyServer`

+ ClientCalls: process different `Request`
