# Set-TeamsCustomBackgrounds
This Script downloads a set of custom Backgrounds from an Azure Blob and stores it in the appropriate folder in Teams, so that you can centrally distribute corporate backgrounds to your users.

It also logs events to the Application Event Log using this source "Intune-PoSh-SPE-WIN10-Baseline-Devices-Teams-CustomBackgrounds". This makes it easy for you to troubleshoot and trace what the script does when distributing it via Intune for example.

It supports the "classic" Teams client as well as the "New" (beta) client.

# Solution Overview
The Script is being distributed via Intune, so that it runs upon every LogIn/Reboot of a users machine. It checks if the files in the Azure Blob exist in the needed Teams Folder (for old and new). 
If the needed picture does not exist, it downloads it to the according folder.

## Requierments
- You have an Azure Storage Account with a Blob
- You use a SAS that permits the following operations on the container level:
   - List
   - Read
- The files in the Blob have been added manually to "classic" Teams beforehand. You then grab them from the
%AppData%\Microsoft\Teams\Backgrounds\Uploads\ and upload these Files to the Blob (so that it creates the Thumbnail)

Example contents of Blob:
- 01_generic.jpg
- 01_generic_thumb.jpg


# "Classic" Teams vs. "New" Teams client
There are different requierments for these two clients so that the Teams Background Pictures show up in Teams.

## Classic client
In %AppData%\Microsoft\Teams\Backgrounds\Uploads\ a combination of the background picture and its thumbnail to be shown in the selection:
   - 01_generic.jpg
   - 01_generic_thumb.jpg

## New client
In %localAppData%\Packages\MSTeams_8wekyb3d8bbwe\LocalCache\Microsoft\MSTeams\Backgrounds\Uploads a combination of the background picture and its thumbnail to be shown in the selection:
- 0b19f8d7-66d7-8856-ba5a-aaa04a3d309d.jpeg
- 0b19f8d7-66d7-8856-ba5a-aaa04a3d309d_thumb.jpeg

# How-To run the Script
Make sure you define the Variables below according to your situation:


```powershell
$StorageAccountName = "SAC-CustomTeamsBG"
$ContainerName = "custombgs"
$SASToken = "sp=.........."
```

Then you can run the script and verify its working. If it does, simply create an Intune Script (64bit mode) and distribute that to your users.

# Contribution
If you see something worth changing/adding, feel free to open a PR :)

