# FNA VSCode Template
Start new FNA projects with Nez quickly and easily with handy setup scripts, a versatile boilerplate project, and convenient Visual Studio Code integration.


## Features ##
- Super simple setup scripts that download and install Nez, FNA and its native libraries for you
- Boilerplate project already included -- no need to wrestle with MSBuild configurations or writing yet another Game1 class
- Visual Studio Code tasks for building and running your game, cleaning/restoring your project, compiling .fx files and building content with the MonoGame Pipeline tool
- In-editor debugging support with the Mono Debugger


## Prerequisites ##
- [Visual Studio Code](https://code.visualstudio.com)
  - [Mono Debugger Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.mono-debug) (required for macOS debugging)
- [Git](https://git-scm.com)
- [Microsoft DirectX SDK (June 2010)](https://www.microsoft.com/en-us/download/details.aspx?id=6812) (required for building effects -- on Mac, [you can use Wine to run this](https://github.com/AndrewRussellNet/FNA-Template#linuxmacos-installing-the-directx-sdk-on-wine))


## Setup Instructions ##
1. Download and unzip the ZIP archive (don't clone the repo!)
2. Run `./getFNA.sh` (macOS) to download the latest Nez, FNA and fnalibs to the directory. You can run this script again if you want to update either FNA or the fnalibs at a later point. Nez is setup as a submodule so you can update it in the normal fashion.
3. Open the newly-created and named `PROJECT_NAME_YOU_CHOSE.code-workspace` file (or open the project folder in Visual Studio Code or the top-level sln in Visual Studio)

That's it! Now you're ready to build and run the base project. When developing raw content (files not processed by the Pipeline tool) should be placed in the `Content` folder and anything that needs processing should go in the `CompiledContent` folder and added to the Pipeline tool.

If you want to see the output of `Debug.*` calls in the VS Code Debug Console, you have to install a listener by adding this somewhere in your code (Game1 is a good spot): `System.Diagnostics.Debug.Listeners.Add(new System.Diagnostics.TextWriterTraceListener(System.Console.Out));`


## Build Tasks ##
- **Restore Project:** Restores the .csproj. Run it again whenever you change the .csproj file.
- **Build (Debug/Release):** Builds the project with the specified configuration but does not run it. This also runs MGCB.exe, copies over everything in the `Content` and `CompiledContent` subdirectories and the fnalibs.
- **Build and Run (Debug/Release):** Builds and runs the project. On MacOS, it runs the output with Mono. On Windows, it runs the output with .NET Framework.
- **Clean Project:** Cleans the output directories and all their subdirectories.
- **Build Effects:** Runs `fxc.exe` on all of the `.fx` files found in the Content/ subdirectories and outputs corresponding `.fxb` files that can be loaded through the Content Manager at runtime.
- **Build Content:** Runs good old MGCB.exe on the Content.mgcb file
- **Force Build Content:** Force builds the content (MGCB.exe -r)
- **Open Pipeline Tool:** Opens the MonoGame Pipeline tool
- **Process T4 Templates:** Processes any T4 templates found in the `T4Templates` folder. Note that the install script will attempt to install the t4 command line program which requires the `dotnet` command line program to be installed. The install command it will run is `dotnet tool install -g dotnet-t4`.


## License and Credits ##
FNA VSCode Template is released under the Microsoft Public License.
Many thanks to Andrew Russell for his [FNA Template](https://github.com/AndrewRussellNet/FNA-Template), from which I learned a lot (and borrowed a little).
