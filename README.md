# Set-TeamsCustomBackgrounds
This Script downloads a set of custom Backgrounds from an Azure Blob and stores it in the appropriate folder in Teams, so that you can centrally distribute corporate backgrounds to your users.

It supports the "classic" Teams client as well as the "New" (beta) client.

## Requierments
- You have an Azure Blob with a SAS that permits the following operations on the container level:
   - List
   - Read
- The files in the Blob have been added manually to "classic" Teams beforehand. You then grab them from the
%AppData%\Microsoft\Teams\Backgrounds\Uploads\ and upload these Files to the Blob (so that it creates the Thumbnail)

Example contents of Blob:
- 01_generic.jpg
- 01_generic_thumb.jpg


# Solution Overview
The Script is being distributed via Intune, so that it runs upon every LogIn/Reboot of a users machine. It checks if the files in the Azure Blob exist in the needed Teams Folder (for old and new). 
If the needed picture does not exist, it downloads it to the according folder.

# Contribution
If you see something worth changing/adding, feel free to open a PR :)




Yes you also need to have a Thumbnail for each background picture. That Thumbnail needs to match the GUID of the background picture:

0b19f8d7-66d7-8856-ba5a-aaa04a3d309d.jpeg
0b19f8d7-66d7-8856-ba5a-aaa04a3d309d_thumb.jpeg
In my approach, I use an Azure Blob to store the pictures with their Thumbail (I add them manually to "classic" Teams beforehand, grab them from the "Uploads" Folder and upload them to the Blob).
Then my PowerShell Script (distributed via Intune) downloads all Files from that Blob. If NewTeamsIsPresent on the System where the Script runs, it downloads the same file as for "classic" Teams but creates a GUID from the Filename. 
