# Bug information

When building this project with a .NET 9 SDK the following error will be generated:

> Restore complete (0.9s)
  classlib net472 failed with 1 error(s) (0.0s)
    C:\Program Files\dotnet\sdk\9.0.101\Sdks\Microsoft.NET.Sdk\targets\Microsoft.PackageDependencyResolution.targets(266,5): error NETSDK1047: Assets file 'C:\Users\jaredpar\temp\example\classlib\obj\project.assets.json' doesn't have a target for 'net472/win-x86'. Ensure that restore has run and that you have included 'net472' in the TargetFrameworks for your project. You may also need to include 'win-x86' in your project's RuntimeIdentifiers.
  console succeeded (0.2s) → console\bin\Debug\net9.0\console.dll
  classlib net9.0 succeeded (0.1s) → classlib\bin\Debug\net9.0\classlib.dll

Thus far I've been unable to determine what causes this error. However if you add the following line to `classlib.csproj` the error will go away:

```xml
<OutputType>Exe</OutputType>
```

Interestingly this is actually add unconditionally by one of the props files from the xunit package but it's not early enough to fix this.