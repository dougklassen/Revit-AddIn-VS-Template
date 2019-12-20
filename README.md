# Revit Add-In Template
-----

## Overview

This is a Visual Studio project template for creating Revit add-in applications and commands. It includes a command and a startup application. The application adds a button to the ribbon that will launch the command when clicked. Embedded images are included for use as command icons.

The project is configured with builds targetting Revit 2014 through Revit 2020. Each supported version of Revit has its own Visual Studio build configuration named after the version, e.g. ```Rvt2020```.

When Revit is run it looks for ```.addin``` manifest files to use for loading addins. It uses these manifests to load classes from ```.dll``` files that provide addin commands and applications. This template is based on deploying an addin manifest to ```C:\ProgramData\Autodesk\Revit\Addins\<Version Number>\``` and the ```.dll``` containing the class library to ```C:\ProgramData\Autodesk\Revit\Addins\<Version Number>\<Addin Name>\<Addin Name>.dll```.

## Important Files

- ```\Resources\NewAddIn.addin```: The manifest file used by Revit to load the addin. This file is copied the addin directory which Revit checks every time it runs. 
- ```\RevitAddInTemplate.csproj```: This is the ```.csproj``` file for the project. It has been edited to support Revit addin development:
    - A line has been added to circumvent a restriction in Visual Studio that prevents adding WPF windows to a class library project.
    - Build configurations are defined for every version of Revit from 2014 onwards.
    - The project will be built against the version of the .NET framework appropriate for a particular version of Revit
    - References to ```RevitAPI.dll``` and ```RevitAPIUI.dll``` will point to the local installation of the targeted version. Note that this requires that version to be installed on the build machine.
    - Post build events have been added to copy the addin ```.dll``` and ```.addin``` files to the addin folder for the targeted version of Revit. This effectively installs the addin after a sucessful build.
- ```NewAddIn.cs```: A class that defines the addin application loaded by Revit. This class contains code that runs when Revit is started, so it is able to perform tasks such as addding buttons to the ribbon.
- ```\Resources\NewCommand.cs```: A class that defines an addin command run ineractively by the user, e.g. using a button on the ribbon.

## Configuring your project

- ### In *Project Properties*:
    - Change the *Assembly Name* from ```NewAddIn```
    - Change the *Default Namespace* from ```DougKlassen.Revit.NewAddIn```
    - Update the fields in the *Assembly Information* dialog
- ### Update the ```StartUpApp.cs``` file:
    - Update the namespace declaration.
    - Within the ```FileLocations``` class, update the value of ```ResouceNameSpace``` per the correct namespace.
    - Within the ```StartUpApp``` class, update ```newCommandPushButtonData``` to correspond to your actual addin command.
- ### Update the ```\Commands\NewCommand.cs``` file:
    - Rename the file to match the name of your addin's command
    - Rename the class ```NewCommand``` with your desired class name
- ### Update the ```\Resources\NewAddIn.addin``` file:
    - Rename the file to match your assembly name
    - Within ```<Command>```, update the ```<Assembly>``` property to match the actual path to your addin's ```.dll``` file.
    - Within ```<Command>```, update the ```<FullClassName>``` property with the fully qualified class name for your command class.
    - Within ```<Command>```, update the ```<Text>``` field with the text that will display on the *External Tools* dropdown button of the *Add-Ins* ribbon.
    - Within ```<Application>```, update the ```<Assembly>``` property to match the actual path to your addin's ```.dll``` file.
    - Within ```<Application>```, update the ```<FullClassName>``` property with the fully qualified class name for your application's startup class.
    - Update ```<VendorId>``` and ```<VendorDescription>``` fields with correct information. Note these fields will be displayed by Revit if your addin throws an exception. 
    - Update ```<AddInId>``` with a new GUID.