# winiot--custom-noobs
To make a custom version of NOOBS that will provide a way to create a factory restore feature for customized Windoes 10 IoT images.

This repo is created to try to make a custom version of NOOBS for Raspberri Pi that will implement a factory restore process to be used with customize commercial Windows 10 IoT images.

Based on the reading of NOOBS, this SHOULD work, but the resulting installation fails for some reason that I can't explain at the moment. Perhaps the community will notice a flaw and contribute.

You will need:
1. Notepad++ or other editor that can maintain the unix line endings.
2. WinRAR or some other archiver program capable of extracting *.tar.xz files.
3. SD Association's Formatting Tool from https://www.sdcard.org/downloads/formatter_4/eula_windows/.

Here's what you do:
NOTE: Unix files are case sensitive. Make sure you get file and folder named right.

1. Set up the base NOOBS folders:
   a. Download NOOBS_Lite from raspberrypi.org and extract it to C:\WinIoT-NOOBS\.   
2. Prepare NOOBS:

   a. Create the folders for your custom os:
   
      i. Create a folder "C:\WinIoT-NOOBS\os\".
      
      ii. Create a folder "C:\WinIoT-NOOBS\os\Windows_IoT\".
      
   b. Get the default scripts:
   
      i. NOOBS loads it's os image list from: http://downloads.raspberrypi.org/os_list_v3.json. So browse to that URL and find the Windows IoT section. It begins with: "os_name": "Windows 10 IoT Core".
      
      ii. Download the files indicated for: icon, marketting_info, os_info, partitions_info, partition_setup and tarballs and copy them into "C:\WinIoT-NOOBS\os\Windows_IoT\".
      
      iii. If your browser displays any json or sh files as text, manually copy the text into the appropriate file names.
      
      iv. Use a tool to convert the line endings of the json and sh files to unix line endings, or use Notepad++ to do it.
      
      v. Extract the "marketting.tar" file to "C:\WinIoT-NOOBS\os\Windows_IoT\". I used WinRAR. This should create a folder called "C:\WinIoT-NOOBS\os\WinIoT\slides_vga\" with several png files in it.
      
   c. Add the Windows 10 IoT ISO image:
   
      i. Download the latest Windows 10 IoT for Raspberry Pi 2&3 ISO file and copy it to "C:\WinIoT-NOOBS\os\MyWinIoT\".
      
      ii. Change it's name to "IOT Core RPi.ISO"
      
   d. Using Notepad++ edit the "partition_setup.sh" file:
   
      i. Change the IMAGE= line near the beginning od the script to:
         IMAGE="/mnt/os/Windows_IoT/IOT Core RPi.ISO"

      ii. Find the if..fi section that refers to DEBUG and InstallationPrecheck. Add '#' characters to the beginning of all those lines to comment them out, or simpley delete them. That section brings up a loader that asks you to download the release or insider version. We will not be downloading.
      
      iii. The next if..fi section downloads the version selected. You will see a comment about downloading the ISO and a "wget" command. Comment out all of this section too or simpley delete them.
      
      iv. Make sure you have unix line endings enabled and save the file.
      
   e. Using Notepad++ edit the "os.json" file:
   
      i. Change "Name": property to "My Windows 10 IoT Core Image" or some other name so that it is differentiated from the one NOOBS downloads if the RPi happens to be connected to the internet when it starts.
      
      ii. Make sure you have unix line endings enabled and save the file.
      
   f. Using Notepad++ edit the "partitions.json" file:
   
      i. Make sure that you have unix line endings enabled and save the file.
      
3. Create the SD card:

   a. Insert an SD card that is 8GB or greater in size into your computer.
   
   b. Format the SD card:
   
      i. Download the SD Association's Formatting Tool from https://www.sdcard.org/downloads/formatter_4/eula_windows/.
      
      ii. Install and run the Formatting Tool on your machine.
      
      iii. Set "FORMAT SIZE ADJUSTMENT" option to "ON" in the "Options" menu.
      
      iv. Check that the SD card you inserted matches the one selected by the Tool.
      
      v. Click the "Format" button.
      
   c. Copy the files in "C:\WinIoT-NOOBS\" to the root of the SD card.

