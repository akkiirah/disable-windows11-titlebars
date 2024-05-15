# Disable Windows11 Titlebars
This PowerShell script overrides the title bar style of all currently open windows to remove them.  
Please note that this script only works with standard Windows 11 title bars.  
Title bars from most browsers or Visual Studio / Visual Studio Code will not be affected.
![image](https://github.com/akkiirah/disable-windows11-titlebars/assets/46369555/3214e368-da4a-41b1-9cf7-5f3bcc65e743)
![image](https://github.com/akkiirah/disable-windows11-titlebars/assets/46369555/83e11895-87a5-4817-8171-ff90300dd9d9)

I want to address that I'm not an expert programmer, nor do I have much experience in scripting with PowerShell.  
If you want to improve my code, feel free to do so!  
Since I've been wanting to disable the title bar for a while now, I hacked together something that seems to work, at least for me.

-----

### Prerequisites  
- PowerShell
- Some kind of texteditor
- Administrator rights on your user.

-----

### Installation
- Download the ZIP file and unpack its contents to a location of your choice, preferably somewhere with a short path.
- Open the `DeleteTitlebar.bat` file with the text editor of your choice and change `C:\Users\akkiirah\.glaze-wm\scripts\DeleteTitlebar.ps1` to the path where you unpacked the files.

-----

### How to use:
- You can now simply run the `DeleteTitlebar.bat` file, which will remove all standard Windows 11 title bars.  
If you wish to have a shortcut to this batch file in your Start menu, create a shortcut and place it inside a folder that you can access through the Start menu.  
This way, you can pin a batch file to the Start menu.

- However, I would recommend using some kind of hotkey daemon to call this script whenever you open a new window where you wish the title bar to disappear.  
Since I'm using GlazeWM, this is how I call this script.

```yaml
  - command: 'exec C:\Users\akkiirah\.glaze-wm\scripts\DeleteTitlebar.bat'
    binding: 'Alt+Ctrl+Space'
```
-----

### One more tip:
- For some reason, this script doesn't completely remove the title bar. There will still be around 10 pixels left.  
It is possible to reduce this to almost 0 by changing `PaddedBorderWidth` to 0 in `Computer\HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics` in your registry.  
> However i must inform you that editing your registry might produce unwanted side effects or endanger your system.  
Edit the registry at your own risk!

Also note, if you're running GlazeWM with GAPS, setting `PaddedBorderWidth` to 0 seems to make all standard windows containers not adjust acording to your set gap.  
To fix this, I apply the window rule to resize borders left, right and bottom minus your gap size and match it to every process.  
However you can also adjust the match_process_name to the windows that are making issues. I was to lazy for that so far.  

```yaml
  - command: 'resize borders 0px [your gap]px [your gap]px [your gap]px'
    match_process_name: '.*'
```
-----

### TODO:
- Find a way to supress opening a powershell window when running the script.
- Let the script run in the background and update the titlebar of newly opend windows automatically.
- Find a way to completly hide the titlebar. No single pixel shall live.
-----