# Getting `Google Agents CLI` to work on Windows 10

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
- Added this directory ``"C:\Users\<user>\.local\bin` to User's PATH variable. 
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
