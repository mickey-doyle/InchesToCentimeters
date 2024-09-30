## InchesToCentimeters

very simple program that converts inches to centimeters.

- there are binary versions of this program for macOS (ARM) and Windows. see [releases](https://github.com/mickey-doyle/InchesToCentimeters/releases)

- depends on .NET 8.0 runtime and Gtk# 3 (only required if building from source)

if building on macOS, run the following first:
```zsh
brew install --cask dotnet-sdk && brew install gtk+3
```


## Program.cs
```csharp
using System;
using Gtk; // for cross platform support since my pc isn't working and i cant bear working in a VM anymore =)

static class InchesToCentimeters
{
    static void Main()
    {
        Application.Init();

        // new window
        var window = new Window("inches to centimeters");
        window.SetDefaultSize(300, 150);
        window.DeleteEvent += delegate { Application.Quit(); };

        // layout 
        var vbox = new Box(Orientation.Vertical, 5);
        var input_label = new Label("how many inches:");
        var inches_entry = new Entry();
        var convert_button = new Button("convert to cm");
        var result_label = new Label();

        // add widgets
        vbox.PackStart(input_label, false, false, 5);
        vbox.PackStart(inches_entry, false, false, 5);
        vbox.PackStart(convert_button, false, false, 5);
        vbox.PackStart(result_label, false, false, 5);
        window.Add(vbox);

        // button click functionality
        convert_button.Clicked += (sender, e) =>
        {
            if (double.TryParse(inches_entry.Text, out double inches))
            {
                // conversion
                double centimeters = inches * 2.54;
                result_label.Text = $"{inches}in = {centimeters}cm";
            }
            else
            {
                result_label.Text = "try entering a number, chief";
            }
        };

        // show widgets
        window.ShowAll();

        Application.Run();
    }
}

```

