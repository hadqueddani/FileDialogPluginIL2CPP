# FileDialogPluginIL2CPP
Unity IL2CPP File Dialog Plugin (.dll)

Small .dll file to open and save files from Unity using IL2CPP as Scripting Backend.

[Microsoft Visual C++ Redistributable] IS REQUIRED FOR THE PLUGIN TO WORK PROPERLY.

```csharp
using System;
using System.Runtime.InteropServices;
using UnityEngine;
public class FileBrowser : MonoBehaviour
{
    [DllImport("FileDialogPluginIL2CPP.dll", CharSet = CharSet.Unicode)]
    private static extern IntPtr OpenFileDialog([MarshalAs(UnmanagedType.LPWStr)] string filter);

    [DllImport("FileDialogPluginIL2CPP.dll", CharSet = CharSet.Unicode)]
    private static extern IntPtr SaveFileDialog([MarshalAs(UnmanagedType.LPWStr)] string filter);

    public void OpenFileBrowserSong()
    {
        string filter = "All Files\0*.*\0Audio Files\0*.wav;*.mp3;*.ogg\0";

        IntPtr ptr = OpenFileDialog(filter);

        string path = Marshal.PtrToStringUni(ptr);

        if (!string.IsNullOrEmpty(path))
        {
            Debug.Log(path);
        }
    }

    public void SaveToPath()
    {
        string filter = "CSV File\0*.csv\0Text File\0*.txt\0";

        IntPtr ptr = SaveFileDialog(filter);

        string path = Marshal.PtrToStringUni(ptr);

        if (!string.IsNullOrEmpty(path))
        {
            if (!path.EndsWith(".csv"))
            {
                path += ".csv";
            }

            ValuesToExport(new string[] { path });
        }
        else
        {
            Debug.Log("Canceled.");
        }
    }
}
