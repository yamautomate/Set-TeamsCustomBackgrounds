# Set-TeamsCustomBackgrounds
This Script downloads a set of custom Backgrounds from an Azure Blob and stores it in the appropriate folder in Teams, so that you can centrally distribute corporate backgrounds to your users.

It supports the "classic" Teams client as well as the "New" (beta) client.

The script assumes the following:
- The files in the Azure Blob Storage have been added to Teams manually (so that it creates the Thumbnail) and then have been added to the Blob. 
- So the Blob holds the final pictures to distribute together with its Thumbnail

# Contribution
If you see something worth changging/adding, feel free to open a PR :)
