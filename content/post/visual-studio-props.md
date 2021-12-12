+++
author = "I am"
title = "Шпаргалка по созданию простейшего файла проекта .vcxproj Visual Studio"
date = "2019-03-05"
description = "Visual Studio props"
tags = [
    "Visual Studio",
    "vcxproj",
    "props",
]
+++

## Вынос настроек проекта в .props файлы

**.vcxproj** - это обычный XML-документ и его можно логически разделить на две части:

* сам **.vcxproj** файл, содержащий список включенных в проект исходных файлов
* файл **.props**, содержащий настройки проекта


**.vcxproj**

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project DefaultTargets="Build" ToolsVersion="12.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(SolutionDir)\settings.props" />
  <PropertyGroup Label="Globals">
    <ProjectGuid>{0D35456E-42DA-418B-87D4-55E32B8E1373}</ProjectGuid>
    <TargetFrameworkVersion>v4.5</TargetFrameworkVersion>
  </PropertyGroup>
  <ItemGroup>
    <ClInclude Include="module.h" />
    <ClCompile Include="module.cpp" />
  </ItemGroup>
</Project>
```

**settings.props**

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <ItemGroup>
    <ProjectConfiguration Include="Debug|Win32">
      <Configuration>Debug</Configuration>
      <Platform>Win32</Platform>
    </ProjectConfiguration>
    <ProjectConfiguration Include="Release|Win32">
      <Configuration>Release</Configuration>
      <Platform>Win32</Platform>
    </ProjectConfiguration>
  </ItemGroup>

  <PropertyGroup>
    <ConfigurationType>Application</ConfigurationType>
    <PlatformToolset>v120</PlatformToolset>                      -- VS 2013
  </PropertyGroup>

  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.default.props" />
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />

  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />

  <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'">
    <ClCompile>
      <Optimization>Disabled</Optimization>
      <DebugInformationFormat>EditAndContinue</DebugInformationFormat>
    </ClCompile>
    <Link>
      <GenerateDebugInformation>true</GenerateDebugInformation>
    </Link>
  </ItemDefinitionGroup>

</Project>
```
