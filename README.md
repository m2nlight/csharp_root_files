CSharp Root Files
=================

- [CSharp Root Files](#csharp-root-files)
  - [.gitignore](#gitignore)
  - [.csharpierignore](#csharpierignore)
    - [Xaml/Axaml Formatter](#xamlaxaml-formatter)
  - [.editorconfig](#editorconfig)
    - [SpellingExclusions.dic](#spellingexclusionsdic)
    - [Meziantou.Analyzer](#meziantouanalyzer)
  - [Directory.Build.props](#directorybuildprops)
  - [Directory.Packages.props](#directorypackagesprops)
- [Some useful properties in csproj](#some-useful-properties-in-csproj)
  - [MSBuild Properties](#msbuild-properties)
  - [Condition](#condition)
  - [MSBuild Targets](#msbuild-targets)

.gitignore
----------

Create a .gitignore file for the dotnet projects.

```sh
dotnet new gitignore
```

.csharpierignore
----------------

This file is used to ignore formatting _xml files_ from csharpier.

**Install csharpier**

```sh
dotnet tool install --global csharpier
```

**Install Extensions**

- Visual Studio: [CSharpier](https://marketplace.visualstudio.com/items?itemName=csharpier.CSharpier)
- Rider: [csharpier](https://plugins.jetbrains.com/plugin/18243-csharpier/versions/stable)
- VSCode: [CSharpier - Code formatter](https://marketplace.visualstudio.com/items?itemName=csharpier.csharpier-vscode) , ID `csharpier.csharpier-vscode`

### Xaml/Axaml Formatter

**Install Extensions**

- Visual Studio: [XAML Styler for Visual Studio 2022](https://marketplace.visualstudio.com/items?itemName=TeamXavalon.XAMLStyler2022)
- Rider: [XAML Styler](https://plugins.jetbrains.com/plugin/14932-xaml-styler/versions)
- VSCode: [XAML Styler](https://marketplace.visualstudio.com/items?itemName=dabbinavo.xamlstyler) , ID `dabbinavo.xamlstyler`

.editorconfig
-------------

Create a new .editorconfig file by dotnet new command.

```sh
dotnet new editorconfig
```

Then add spelling_exclusion_path to `[*]` section

```editorconfig
[*]
spelling_exclusion_path = SpellingExclusions.dic
```

### SpellingExclusions.dic

Each line is a word to exclude from spelling check.

The filename is an option `spelling_exclusion_path` from `.editorconfig` file.

### Meziantou.Analyzer

https://github.com/meziantou/Meziantou.Analyzer

<details>
<summary>Add severity configurations to .editorconfig</summary>

```editorconfig
[*.cs]
# https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/configuration-options#severity-level
# error, warning, suggestion, silent, none, default
dotnet_diagnostic.MA0002.severity = suggestion
dotnet_diagnostic.MA0004.severity = suggestion
dotnet_diagnostic.MA0005.severity = silent
dotnet_diagnostic.MA0006.severity = suggestion
dotnet_diagnostic.MA0008.severity = suggestion
dotnet_diagnostic.MA0009.severity = suggestion
dotnet_diagnostic.MA0011.severity = suggestion
dotnet_diagnostic.MA0015.severity = error
dotnet_diagnostic.MA0016.severity = suggestion
dotnet_diagnostic.MA0017.severity = error
dotnet_diagnostic.MA0019.severity = suggestion
dotnet_diagnostic.MA0021.severity = suggestion
dotnet_diagnostic.MA0022.severity = suggestion
dotnet_diagnostic.MA0023.severity = suggestion
dotnet_diagnostic.MA0024.severity = suggestion
dotnet_diagnostic.MA0028.severity = suggestion
dotnet_diagnostic.MA0033.severity = error
dotnet_diagnostic.MA0046.severity = suggestion
dotnet_diagnostic.MA0047.severity = error
dotnet_diagnostic.MA0048.severity = suggestion
dotnet_diagnostic.MA0051.severity = suggestion
dotnet_diagnostic.MA0054.severity = error
dotnet_diagnostic.MA0055.severity = suggestion
dotnet_diagnostic.MA0056.severity = suggestion
dotnet_diagnostic.MA0057.severity = error
dotnet_diagnostic.MA0058.severity = error
dotnet_diagnostic.MA0059.severity = warning
dotnet_diagnostic.MA0061.severity = suggestion
dotnet_diagnostic.MA0062.severity = error
dotnet_diagnostic.MA0064.severity = error
dotnet_diagnostic.MA0070.severity = suggestion
dotnet_diagnostic.MA0074.severity = suggestion
dotnet_diagnostic.MA0076.severity = none
dotnet_diagnostic.MA0077.severity = suggestion
dotnet_diagnostic.MA0081.severity = error
dotnet_diagnostic.MA0084.severity = error
dotnet_diagnostic.MA0085.severity = error
dotnet_diagnostic.MA0091.severity = suggestion
dotnet_diagnostic.MA0092.severity = error
dotnet_diagnostic.MA0093.severity = suggestion
dotnet_diagnostic.MA0096.severity = suggestion
dotnet_diagnostic.MA0097.severity = suggestion
dotnet_diagnostic.MA0099.severity = error
dotnet_diagnostic.MA0100.severity = error
dotnet_diagnostic.MA0134.severity = suggestion
dotnet_diagnostic.MA0146.severity = suggestion
dotnet_diagnostic.MA0158.severity = suggestion
dotnet_diagnostic.MA0168.severity = warning
dotnet_diagnostic.MA0191.severity = suggestion
dotnet_diagnostic.MA0195.severity = error
dotnet_diagnostic.MA0196.severity = error
dotnet_diagnostic.MA0198.severity = error
dotnet_diagnostic.MA0199.severity = error
dotnet_diagnostic.MA0201.severity = suggestion
dotnet_diagnostic.MA0203.severity = error
dotnet_diagnostic.MA0207.severity = error
dotnet_diagnostic.MA0208.severity = error
```

</details>


Directory.Build.props
---------------------

Some common settings for dotnet projects.

- Product Version for CLI (_not supported in MAUI_)
- Product Information (_not supported in MAUI_)
- DefineConstants for CLI
- OutputPath
- [Nullable Reference Types (NRT)](https://learn.microsoft.com/en-us/dotnet/csharp/nullable-references)
- [CSharp Language Version](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version)
- ImplicitUsings
- NuGetAudit for Release
- [NETSDK1206 Warning](https://learn.microsoft.com/en-us/dotnet/core/tools/sdk-errors/netsdk1206)
- Type Alias

Directory.Packages.props
------------------------

[Central Package Management (CPM)](https://learn.microsoft.com/en-us/nuget/consume-packages/central-package-management) configuration file.

- ManagePackageVersionsCentrally
- CentralPackageTransitivePinningEnabled
- CentralPackageVersionOverrideEnabled
- CentralPackageFloatingVersionsEnabled
- PackageVersion
- Meziantou.Analyzer
- PolySharp

**VersionOverride** can be used to override the version of a package in a `csproj` file.

```xml
<ItemGroup>
  <PackageReference Include="PackageName" VersionOverride="1.0.0-rc.1" NoWarn="NU1605" />
</ItemGroup>
```

`NoWarn="NU1605"` for ignored package downgrade warning.
See [NuGet Warning NU1605](https://learn.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu1605)

# Some useful properties in csproj

## MSBuild Properties

See [MSBuild reference for .NET SDK projects](https://learn.microsoft.com/en-us/dotnet/core/project-sdk/msbuild-props)

```xml
<PropertyGroup>
  <UseWinForms>true</UseWinForms>
  <UseWPF>true</UseWPF>

  <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  <ApplicationManifest>app.manifest</ApplicationManifest>

  <SelfContained>true</SelfContained>
  <RuntimeIdentifier>win-x64</RuntimeIdentifier>
  <SatelliteResourceLanguages>zh-Hans</SatelliteResourceLanguages>
  <PublishDocumentationFile>true</PublishDocumentationFile>

  <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
  <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
</PropertyGroup>
```

## Condition

**Condition property** can be used

- PropertyGroup
- ItemGroup
- Target
- When


```xml
<Target Name="CopyNLogConfig" AfterTargets="AfterBuild">
  <Copy SourceFiles="NLog.config" DestinationFiles="$(OutDir)NLog.config" SkipUnchangedFiles="false" Condition="'$(Configuration)'!='Debug'" />
  <Copy SourceFiles="NLog.Debug.config" DestinationFiles="$(OutDir)NLog.config" SkipUnchangedFiles="true" Condition="'$(Configuration)'=='Debug'" />
</Target>
```

**Choose-When-Otherwise** property group

```xml
<Choose>
  <When Condition="'$(DefineConstants.Contains(`SomeConstant`))' == 'true' and '$(DefineConstants.Contains(`OtherConstant`))' == 'false'">
    <ItemGroup>
      <PackageReference Include="PackageNameA" />
    </ItemGroup>
  </When>
  <When Condition="'$(DefineConstants.Contains(`SomeConstant`))' == 'true' and '$(DefineConstants.Contains(`OtherConstant`))' == 'true'">
    <ItemGroup>
      <PackageReference Include="PackageNameB" />
    </ItemGroup>
  </When>
  ...
  <Otherwise>
    <ItemGroup>
      <PackageReference Include="PackageNameC" />
    </ItemGroup>
  </Otherwise>
  </Choose>
```

## MSBuild Targets

- [Targets](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-targets)
  * [Target build order](https://learn.microsoft.com/en-us/visualstudio/msbuild/target-build-order)

    * DependsOnTargets
    * AfterTargets
    * BeforeTargets

- [Tasks](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-tasks)

  * [Message task](https://learn.microsoft.com/en-us/visualstudio/msbuild/message-task)
  * [Copy task](https://learn.microsoft.com/en-us/visualstudio/msbuild/copy-task)
  * [Delete task](https://learn.microsoft.com/en-us/visualstudio/msbuild/delete-task)
  * [MakeDir task](https://learn.microsoft.com/en-us/visualstudio/msbuild/makedir-task)
  * [RemoveDir](https://learn.microsoft.com/en-us/visualstudio/msbuild/removedir-task)
  * [Move task](https://learn.microsoft.com/en-us/visualstudio/msbuild/move-task)
  * ...

```xml
<Target Name="GlobalUniqueTargetName" AfterTargets="AfterBuild;CopyNLogConfig" DependsOnTargets="CopyNLogConfig">
  <ItemGroup>
    <_GlobalUniqueNodeName Include="$(OutDir)models/*" />
  </ItemGroup>

  <Message Importance="high" Text="Move models/* to data..." />
  <MakeDir Directories="$(OutDir)data" />
  <Move SourceFiles="@(_GlobalUniqueNodeName)" OverwriteReadOnlyFiles="true" DestinationFolder="$(OutDir)data" />

  <Message Text="Clean $(OutDir)..." />
  <RemoveDir Directories="$(OutDir)Temp" />
  <Delete Files="$(OutDir)**/*.pdb" />
</Target>
```
