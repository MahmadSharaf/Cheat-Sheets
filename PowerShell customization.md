# Power Shell customization

oh-my-posh is a PowerShell module which helps to decorate our PowerShell window using different in-built and self-customized themes. posh-git is a PowerShell module that integrates Git and PowerShell by providing Git status summary information that can be displayed in the PowerShell prompt.

## Install PowerShell

- First you need to install the latest PowerShell from Microsoft Store

## Module Installation

1. [Oh-my-Posh](https://ohmyposh.dev/docs/windows)
   1. Installation

        ```cmd
        winget install JanDeDobbeleer.OhMyPosh
        ```

   2. Add to Path variables

    `~\AppData\Local\Programs\oh-my-posh\bin\oh-my-posh.exe`

2. Installation of posh-git

    ```cmd
    Install-Module posh-git
    ```

## Customization

### Fonts

   1. Install fonts
      - Choose from this [website](https://www.nerdfonts.com/font-downloads)
      - Choose `Caskaydia Cove Nerd Font`

   2. Apply font
      - Right-click on the PowerShell window top-bar for more options, go to Properties and then to Font.
      - Select `Caskaydia Cove NF` from the available options and click OK

### Themes

   1. Choose Theme
      - Check for available themes, `Get-PoshThemes`
      - Or get this [theme](https://gist.github.com/shanselman/1f69b28bfcc4f7716e49eb5bb34d7b2c?WT.mc_id=-blog-scottha)

   2. Apply Theme:
      - A custom one `oh-my-posh --init --shell pwsh --config ~/jandedobbeleer.omp.json | Invoke-Expression`

## Creating a profile file

1. Open or create a file

    ```cmd
    if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }notepad $PROFILE
    ```

2. Add the commands in notepad

    ```txt
    oh-my-posh --init --shell pwsh --config ~/jandedobbeleer.omp.json | Invoke-Expression
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
- [Scott Hanselman](https://www.hanselman.com/blog/my-ultimate-powershell-prompt-with-oh-my-posh-and-the-windows-terminal)