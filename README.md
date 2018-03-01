Revit2014AddInTemplate
==========================

This is a Visual Studio project template for creating a Revit 2014 add-in application or command. It includes one
command and a startup application which creates a default button for the command on the ribbon. Embedded images are also included for use as command icons.

An .addin file that loads the command and the application is included.

The ProjectTypeGuids setting in the .csproj file has been tinkered with to circumvent a restriction in Visual Studio Express that prevents adding WPF windows to a class library project.
