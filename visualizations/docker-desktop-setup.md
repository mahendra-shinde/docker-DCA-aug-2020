## Docker Desktop on Windows 10 PRO

### Requirements
- Windows 10 PRO or ENT
- Enable Virtualization from System BIOS

## Installation Steps
- Install Hyper-V & Containers Optional Features
- Install Docker Desktop

## Installation Script [Powershell with Administrator Mode]

1.  Enable HyperV and Containers [Optional Windows Features]

    ```pwsh
    $ Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All -NoRestart 
    $ Enable-WindowsOptionalFeature -Online -FeatureName Containers -All -NoRestart
    $ Restart-Computer
    ```

2.  Using "chocolatey" install the docker-desktop.

    ```pwsh
    $ Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    $ choco install docker-desktop -y
    # VSCode,Git Installation (Ignore if already installed!)
    $ choco install vscode git -y
    $ Restart-Computer
    ```

3.  Post Restart, Goto Start Menu and Search for "Docker Desktop" > Click "Docker Desktop" and Wait for approx. 10/15 Minutes for "Docker Desktop" to setup "Linux VM" for linux mode.



