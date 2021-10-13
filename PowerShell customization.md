# Power Shell customization

oh-my-posh is a PowerShell module which helps to decorate our PowerShell window using different in-built and self-customized themes. posh-git is a PowerShell module that integrates Git and PowerShell by providing Git status summary information that can be displayed in the PowerShell prompt.

## Module Installation

1. Installation of oh-my-posh

    ```cmd
    Install-Module oh-my-posh
    ```

2. Installation of posh-git

    ```cmd
    Install-Module posh-git
    ```

## Import modules

```cmd
Import-Module oh-my-posh
Import-Module posh-git
```

## Customization

1. Install fonts
   1. Download all fonts

        ```cmd
        <!-- Download fonts -->
        Invoke-WebRequest -Uri 'https://github.com/powerline/fonts/archive/master.zip' -OutFile .\powerlinefonts.zip
        <!-- Extract fonts zipped file -->
        Expand-Archive .\powerlinefonts.zip
        <!-- Bypass restriction -->
        Set-ExecutionPolicy Bypass
        <!-- Install fonts -->
        .\powerlinefonts\fonts-master\install.ps1
        <!-- Remove unneeded files/folders -->
        Remove-Item .\powerlinefonts.zip
        Remove-Item .\powerlinefonts -Recurse
        ```

   2. Choose from this [website](https://www.nerdfonts.com/font-downloads)
   3. Download this font [agave Nerd Font Mono r](https://en.m.fontke.com/font/64963297/download/)

2. Choose font

   - Right-click on the PowerShell window top-bar for more options, go to Properties and then to Font.
   - Select `agave Nerd Font Mono r` from the available options and click OK

3. Choose Theme

- Check for available themes, `Get-PoshThemes`
- Set the chosen theme, `Set-PoshPrompt -Theme Agnoster`

## Creating a profile file

1. Open or create a file

    ```cmd
    if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }notepad $PROFILE
    ```

2. Add the commands in notepad

    ```txt
    Import-Module oh-my-posh
    Import-Module posh-git
    Set-PoshPrompt -Theme Agnoster
   ```

3. Bonus, add the below commands in the profile

    ```txt
    New-Alias which get-command
    clear
    ```

## Applying font to VSCode

1. Open Settings, `ctrl+,`
2. Search for "Terminal Integrated Font Family"
3. Add Font Name

## References

- [Medium Article](https://medium.com/analytics-vidhya/customize-your-windows-powershell-with-oh-my-posh-posh-git-93284b2749b6)