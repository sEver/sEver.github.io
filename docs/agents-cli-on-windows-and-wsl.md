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
