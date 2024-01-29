# VideoConverter
NetDot Project for converting video files using MediaToolkit (https://github.com/AydinAdn/MediaToolkit/)

# Needs:
1. Dotnet
2. Visual Studio Code
3. Net45
4. C#

Most can be installed from the extensions of the Visual Studio Code. Some will be installed during the initialization process of the project.

# How to initialize dotnet Project
1. Create a directory for your project and navigate there in the terminal
2. Enter the following in the terminal.
```
dotnet new console
dotnet add package MediaToolkit
dotnet add package System.Configuration.ConfigurationManager
```
3. If you're not in the VSCode terminal, you can use ```code .``` to launch the entire directory as a project in VSCode.
4. Next step would be editing the **Program.cs**
5. Copy paste the following code. Example of directory: C:/Users/Admin/Downloads/001/ **Always use forward slash**
```
using System;
using System.IO;
using System.Linq;
using MediaToolkit;
using MediaToolkit.Model;
using MediaToolkit.Options;

class Program
{
    static void Main(string[] args)
    {
        ConvertMovsToMp4("Your Directory", "Your Directory");
    }

    static void ConvertMovsToMp4(string inputDirectory, string outputDirectory)
    {
        // Get all MOV files in the input directory
        var movFiles = Directory.GetFiles(inputDirectory, "*.mov");

        using (var engine = new Engine())
        {
            foreach (var inputFilePath in movFiles)
            {
                // Construct output file path with the same filename but different extension
                var outputFilePath = Path.Combine(outputDirectory, Path.GetFileNameWithoutExtension(inputFilePath) + ".mp4");

                var inputFile = new MediaFile { Filename = inputFilePath };
                var outputFile = new MediaFile { Filename = outputFilePath };

                // Convert the MOV file to MP4
                engine.Convert(inputFile, outputFile);

                Console.WriteLine($"Conversion complete for: {inputFilePath}");
            }
        }

        Console.WriteLine("All conversions complete!");
    }
}
```
6. Then enter the following command to the terminal to start converting your file. 
```
dotnet build
dotnet run
```

Notes:
> The code above is only for .mov to .mp4 video files.
> The directory or folder must only contain .mov files for it to work.
> Can be used as base template for other video file conversions.
