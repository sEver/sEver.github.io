## Getting `Google Agents CLI` to work on Windows 10

Google Agents CLI requires Python 3.11+, Node and `uv`. 
- With `pyenv` installed Python 3.11 by:
  - `pyenv install 3.11`
  - `pyenv global 3.11`
- Then installed the `uv`
  - `pip install uv`
- And with it, installed Google Agents CLI
  - `uvx google-agents-cli setup`
- `agents-cli` command doesn't work. We read up. 
- https://google.github.io/agents-cli/guide/getting-started/ says and we quote: 
  "Platform support: macOS, Linux, and Windows (WSL 2). Native Windows is not officially supported."
- We go to `https://learn.microsoft.com/en-us/windows/wsl/install`
- In our system we do `wsl --install`, there's a nice install log, it installs Ubuntu distro.
- We restart the system and try the `wsl` command.
  
```
PS ...> wsl
Windows Subsystem for Linux has no installed distributions.
You can resolve this by installing a distribution with the instructions below:

Use 'wsl.exe --list --online' to list available distributions
and 'wsl.exe --install <Distro>' to install.
```

- Our `bash` that came with git install ages ago, stopped working. It now seems to be aliased to the `wsl`.

Going through https://learn.microsoft.com/en-us/windows/wsl/install-manual
we run:
- `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
- `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
- `wsl --set-default-version 2`
- `wsl --install`
Got an error:

```
Downloading: Ubuntu
Access is denied.
Error code: Wsl/InstallDistro/E_ACCESSDENIED
```

- Downloaded `https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi`
- Went to `https://apps.microsoft.com/detail/9pdxgncfsczv` and downloaded Ubuntu installer
- It said "The latest version is installed".
- Clicked "Open" and got a console within the installed Ubuntu.
- That works. Executing `bash` now starts a shell inside the WSL Ubuntu distro.
- Turns out more integrating work would be needed to get antigravity to work with `agents-cli` that is inside WSL distro.
- Looked around and turns out that running `uvx` again gives us the list of tools installed
- We can run the installed agents-cli executable with `uvx google-agents-cli`
- Since `agents-cli.exe` was found in `"C:\Users\<user>\.local\bin\agents-cli.exe"` 
  we can add it to PATH the `$env:PATH += ";$env:USERPROFILE\.local\bin"` and it seems to work.
- Added this directory `"C:\Users\<user>\.local\bin` to User's PATH variable. 
- Will monitor for why they said it requires WSL anyway.

To recover our ability to run `git-bash` from command line, without it being overtaken by the `bash` from WSL, we did the following:
- `Edit the system environment variables` Windows App -> Environment Variables -> System Variables -> `Path` -> Edit
- Select `D:\<path to our>\git\usr\bin` and "Move Up" it to the top. Close with `Ok` on all windows.
  - This might actually break something, but will see.

Additionally, we want aliases for this git-bash in both `cmd` and `powershell`, so we do:

For `cmd`
- For CMD we create `c:\Users\<user>\macros.cmd` file with `@doskey git-bash="d:\<path to our>\git\usr\bin\bash.exe" $*`
- Run `regedit` and to a key in `Computer\HKEY_CURRENT_USER\Software\Microsoft\Command Processor` add
- New `String Value` named `AutoRun` with the value of `c:\Users\<user>\macros.cmd`

For PowerShell
- Open `notepad $PROFILE` and add `function git-bash { & "d:\<path to our>\git\usr\bin\bash.exe" @args }`
- If there's no such file, create it: `New-Item -Path $PROFILE -Type File -Force` and try again

Now we have the old git-bash available across the system, we have `bash` executing the git-bash, and if we want the WSL bash, we need to run `wsl`

## Getting `gcloud` to work on Windows 10

This was actually pretty straightforward. 
First we install it according to the https://docs.cloud.google.com/sdk/docs/install-sdk 
By doing in PowerShell: 

```
(New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")
& $env:Temp\GoogleCloudSDKInstaller.exe
```

Since we already have Python 3.11, we uncheck the option to install the bundled one. 

Then we run `gcloud` in the Terminal, only to find out, the system asks us with what program do we want to open this file. 

Turns out, the powershell command installing Google Cloud SDK, gives us a bunch of Python scripts initialized by a bash script.
So to start this, we need to first run our trusty `bash`, and then `gcloud` works. 

But we want our Antigravity to be able to run it on its own. The `gcloud` package comes with its own `install.bat` that supposedly sets up the environment for seemless running in Windows. We run it in classis Windows shell `cmd`. We've received the following error: 

```
'"!PYTHON_CANDIDATE_PATH!"' is not recognized as an internal or external command,
operable program or batch file.
```

When the `>echo %PYTHON_CANDIDATE_PATH%` returns:

```
C:\Users\<user>\AppData\Local\Microsoft\WindowsApps\python.exe
```

That is actually not a Python executable, but a Windows command Alias, that returns: 

```
>C:\Users\<user>\AppData\Local\Microsoft\WindowsApps\python.exe --version
Python was not found; run without arguments to install from the Microsoft Store, or disable this shortcut from Settings > Apps > Advanced app settings > App execution aliases.
```

So we go to `Settings -> Apps -> App execution aliases` where we find two options named "App Installer" with descriptions `python.exe` and `python3.exe`. We turn these off by clicking their switches. 

We retry the `install.bat` script, but now it gives us errors about 

```
'"!PYTHON_CANDIDATE_PATH!"' is not recognized as an internal or external command,
operable program or batch file.
```

Where in fact, where we do `echo %PYTHON_CANDIDATE_PATH%` it actually is the `C:\Users\<user>\.pyenv\pyenv-win\shims\python.bat` file. 
This file was detected by `where python` and treated by the install script as one of the python executable paths. 

After some hacking of the `install.bat` script, we came to the conclusion that there must be a bug in evaluating the `!PYTHON_CANDIDATE_PATH!` value in this particular case, where the evaluation is nested within multiple `IF` and `FOR x IN y DO` blocks and resolves to a .pyenv shim. 
The precise nature of the bug was not determined. 

Moreover, if we supply these shims as the initial value for the `CLOUDSDK_PYTHON` variable, which the script uses as the predefined Python location, then the `install.bat` script just exits silently. 

Following the discoveries by ts-pigeon at https://qiita.com/ts-pigeon/items/6e833ba5afb75dd81b51 (you might need to translate that) we've supplied the actual path of the `python.exe` binary, not the shims, to the `CLOUDSDK_PYTHON` variable and then ran the `install.bat`. 

That made the script work properly. 

It is also believed, that the entire issue could be averted if we chose to install the bundled python together with the Google Cloud SDK.



