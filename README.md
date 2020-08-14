<p align="center">
  <a href="https://sass-lang.com/">
    <img align="center" src="https://user-images.githubusercontent.com/24683383/90129637-49578b00-dd69-11ea-9cac-84f65adaa45d.png" width="200">
  </a>
  <a href="https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor">
    <img align="center" src="https://user-images.githubusercontent.com/24683383/90129570-2b8a2600-dd69-11ea-9a35-52a508451718.png" width="200">
  </a>
</p> 

[//]: # (About)
<h2 align="center"> <b> SCSS in Blazor </b> </h2>
<h4 align="center"> Getting started with SCSS in Blazor </h4>

[//]: # (Pipes)
<p align="center">
  <a href="https://dotnet.microsoft.com/download/dotnet-core" alt="Dotnet core download">
    <img src="https://img.shields.io/badge/dotnet-core--3.1-informational">
  </a>
  <a href="https://github.com/nbprojekt/SCSS-in-Blazor/actions?query=workflow%3A%22Github+CI%22" alt="GitHub CI Status">
    <img src="https://github.com/nbprojekt/SCSS-in-Blazor/workflows/Github%20CI/badge.svg">
  </a>
</p>

<hr>

[//]: # (Nav)
<p align="center">
  <a href="#description"> Description </a> &bull;
  <a href="#pre-requirements"> Pre requirements </a> &bull;
  <a href="#set-up-compiler"> Set up Compiler </a> &bull;
  <a href="#blazor-css-isolation"> Blazor CSS isolation </a>
</p>

<hr>

> **Node: Every step in this repo works for SCSS and SASS the same, there is no difference**  

### Description

This repository guides your through all the steps needed to use SCSS or SASS in your Blazor project.

Also you can open the project in VisualStudio and check out how it works.


### Pre requirements
1. You need [dotnet core 3.1][dotnetCoreDownload] installed
2. An existing Blazor project, if you dont have one you can close [this state][cleanBlazorProject] of the project to get started.
3. [NodeJs][nodeJs] is required to install the SASS Compiler

### Set up Compiler
- First you need to create an `pacakge.json` to be able to install NPM packages:
```
  npm init -y
```
- Now you can install the [SASS Compiler][sassCompiler]
```
npm i node-sass --save-dev
```
- When using NPM you usualy dont want your `node_modules` pushed to your git server.  
  Simply add the following line to your `.gitignore`:  
``` .gitignore
**/node_modules/
```
- For further use you need add an NPM script in your `package.json` to access the compiler binary
``` json
"scripts": {
  ...
  "sass-compiler": "./node_modules/.bin/node-sass"
},
```
- Now we want to use VisualStudio's Pre Build Event to compile our SCSS bevore builing the Blazor app  
  Add this line to your `.csproc`
``` xml
...
<Target Name="PreBuild" BeforeTargets="PreBuildEvent">
  <Exec Command="npm run sass-compiler --  ./{{PATH_TO_PROJECT}}/ -o ./{{PATH_TO_PROJECT}}/" />
</Target>
...
```
> *Tip*: This are just the minimal parameters for the sass compiler, you can check out the [documentation][sassCompilerOptions] to learn more

- _(optional)_ Because we can allways regenerate our SCSS files we can ignore this files  
  The only files we dont ignore are files in the `wwwroot` folder
``` .gitignore
**/*.css
!**/wwwroot/*.css
```

Now your done when you create an SCSS file and Build the project Visual Studio will automaticaly compile your SCSS or SASS files and build the Blazor app.

### Blazor CSS isolation
Comming soon in [DotNet 5.0](https://dotnet.microsoft.com/download/dotnet/5.0)

[dotnetCoreDownload]: https://dotnet.microsoft.com/download/dotnet-core 
[cleanBlazorProject]: https://github.com/NBprojekt/SCSS-in-Blazor/tree/ab66f0498c016bbb2294371f0dbe2f00f5c8770c
[nodeJs]: https://nodejs.org/en/
[sassCompiler]: https://www.npmjs.com/package/node-sass
[sassCompilerOptions]: https://www.npmjs.com/package/node-sass#options
