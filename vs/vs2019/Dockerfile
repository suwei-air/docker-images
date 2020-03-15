# escape=`
FROM mcr.microsoft.com/windows/servercore:ltsc2019
LABEL maintainer="suwei.air@gmail.com"

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Download channel for fixed install.
ARG CHANNEL_URL=https://aka.ms/vs/16/release/channel
ADD ${CHANNEL_URL} C:\TEMP\VisualStudio.chman
# Download the Build Tools bootstrapper.
ADD https://aka.ms/vs/16/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe

# Install Build Tools
RUN C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
      --channelUri C:\TEMP\VisualStudio.chman `
      --installChannelUri C:\TEMP\VisualStudio.chman `
      --add Microsoft.VisualStudio.Workload.VCTools --includeRecommended `
      --add Microsoft.VisualStudio.Component.VC.ATL `
      --installPath C:\BuildTools `
    || IF "%ERRORLEVEL%"=="3010" EXIT 0

# Default to PowerShell if no other command specified.
CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
