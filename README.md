# Revit Add-In Template
==========================

This is a Visual Studio project template for creating a Revit add-in application or command. It includes one
command and a startup application which creates a default button for the command on the ribbon. Embedded images are also included for use as command icons.

An ```.addin``` file that loads the command and the application is included.

The ProjectTypeGuids setting in the ```.csproj``` file has been tinkered with to circumvent a restriction in Visual Studio that prevents adding WPF windows to a class library project.

The project is configured with builds targetting Revit 2014 through Revit 2020. Each supported version of Revit has its own Visual Studio build configuration named after the version, e.g. ```Rvt2020```.

Building will install the add-in on the local machine.
- The ```.addin``` file will be copied to ```--```
- The ```.dll``` will be copied to ```--```

To configure your project

- In project properties
    - Change the *Assembly Name* from ```NewAddIn```
    - Change the *Default Namespace* from ```DougKlassen.Revit.NewAddIn```
- Update the ```NewAddIn.addin``` file
    - Rename the file to match your assembly name
    - change the command name