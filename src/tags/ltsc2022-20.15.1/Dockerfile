# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2022-amd64 AS installer

RUN powershell -Command " `
        $ErrorActionPreference = 'Stop'; `
        $ProgressPreference = 'SilentlyContinue'; `
        `
        iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1')) `
        "

RUN powershell -Command " `
        $ErrorActionPreference = 'Stop'; `
        $ProgressPreference = 'SilentlyContinue'; `
        `
        $env:PATH = 'C:\ProgramData\chocolatey\bin;' + $env:PATH; `
        [Environment]::SetEnvironmentVariable('PATH', $env:PATH, [EnvironmentVariableTarget]::Machine) `
        "

RUN powershell -Command " `
        $ErrorActionPreference = 'Stop'; `
        $ProgressPreference = 'SilentlyContinue'; `
        `
        choco install nodejs --version=20.15.1 -y `
        "

FROM mcr.microsoft.com/windows/nanoserver:ltsc2022

USER ContainerAdministrator
RUN setx /M PATH "%PATH%;C:\Program Files\powershell;C:\Program Files\nodejs"
USER ContainerUser

COPY --from=installer ["/Program Files/nodejs", "/Program Files/nodejs"]
