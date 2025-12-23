# .NET WebAssembly Component Trial

This is a simple C# WebAssembly component built using [componentize-dotnet](https://github.com/bytecodealliance/componentize-dotnet), following the tutorial at https://component-model.bytecodealliance.org/language-support/building-a-simple-component/csharp.html

## Overview

This project demonstrates building a WebAssembly component that exports a simple `add` function.

## Prerequisites

- .NET 10 SDK (preview) or later
- Wasmtime runtime (optional, for testing)
- Windows OS (recommended - Linux/macOS support is experimental)

## Project Structure

- `Component.cs` - Implementation of the add interface
- `wit/component.wit` - WIT (WebAssembly Interface Type) definition
- `adder.csproj` - Project configuration
- `nuget.config` - NuGet package sources (includes dotnet-experimental feed)

## Building

```bash
dotnet build
```

The compiled WebAssembly component will be output to:
```
bin/Debug/net10.0/wasi-wasm/native/adder.wasm
```

## Known Issues

- Linux ARM64 support is currently broken due to bugs in the alpha preview `microsoft.dotnet.ilcompiler.llvm` package
- The project builds successfully on Windows
- macOS and Linux x64 support status is unknown

## WIT Interface

```wit
package docs:adder@0.1.0;

interface add {
    add: func(x: u32, y: u32) -> u32;
}

world example {
    export add;
}
```

## Implementation

The implementation is straightforward:

```csharp
namespace ExampleWorld.wit.exports.docs.adder.v0_1_0;

public class AddImpl : IAdd
{
    public static uint Add(uint x, uint y)
    {
        return x + y;
    }
}
```
