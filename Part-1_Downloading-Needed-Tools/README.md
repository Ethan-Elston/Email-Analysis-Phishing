Notepad++:

	- This is a free and powerful text/code editor for Windows. It's more advanced than the regular Notepad app and is way more useful for programming, scripting, or editing config files.

	- To install it, I first need to head to the notepad-plus-plus website.
		○ https://notepad-plus-plus.org/

![image](https://github.com/user-attachments/assets/53aa4f08-dbff-4521-bb0a-cacbd7de918c)

	- I'll download the latest version, v8.7.9 

	- I need to download Notepad++ for the 64-bit operating system
		○ I'll click the "Installer" link

![image](https://github.com/user-attachments/assets/66aca27a-5d03-437b-a0ea-92fefa584858)

	- Once I open the executable file it will bring me to this Setup window

![image](https://github.com/user-attachments/assets/fde6c86a-5037-4d4d-b4cd-018cbc5fae57)

	- Then I just leave everything in their default settings for the installation, and then click Finish to complete it. 

![image](https://github.com/user-attachments/assets/36bf666f-bc93-44b1-a562-b93122e2b3f0)


HxD:

	- This is a free hex editor for Windows. It lets you view and edit the raw binary data (1s and 0s) of any file, disk, or memory.

	- It's used for:
		○ Editing binary files (like executables, save files, firmware)
		○ Reverse engineering
		○ Digital forensics
		○ Malware analysis
		○ Low-level data recovery
		○ Inspecting raw disk sectors or RAM

	- When I open a file in HxD, I'll see the raw hex values of every bytes inside that file
		○ Hex is used to represent binary data (1s and 0s) in a way that's easier for humans to read
		○ 1 byte = 8 bits = 2 hex digits

	- To start downloading, I'll need to head over to the HxD website
		○ https://mh-nexus.de/en/downloads.php?product=HxD20

![image](https://github.com/user-attachments/assets/4b3d13a7-fc1b-4fc8-9f6b-dabda1794585)

	- I'll need to select the English version and then click the "Download per HTTPs" link

	- Once I unzip the file, I'll need to open the HxDSetup application to get started. I will eventually bring up the setup window

![image](https://github.com/user-attachments/assets/81c2b687-116f-4e87-a69d-1fb55bca4970)

	- Then I just go through the default settings and click install.

 ![image](https://github.com/user-attachments/assets/99da7e47-0e88-4598-a712-74d2eb9c2af8)

ExifTool:

	- A  powerful command-line utility used to view, edit and extract metadata from a wide range of files - mainly images, videos, PDFs, and documents. 

	- Used to:
		○ Extract  metadata such as timestamps, GPS coordinates, camera model, author, software used, etc. 
		○ Identify manipulation by spotting inconsistent or suspicious metadata (a file edited before it was created)
		○ Trace origins of a file or image (where or when it was taken)
		○ Support investigations by revealing hidden or embedded data attackers might overlook  

	- Mainly used in digital forensics to analyze evidence without altering original files


	- I'll need to head to the main website.
		○ https://exiftool.org/index.html

![image](https://github.com/user-attachments/assets/504a8143-ccb3-4f83-981b-cb5772e7fb1c)

	- I'm going to download the Windows Executable version of ExifTool for the 64-bit operating system

	- Once it's finished I'll unzip the file, and open the 'exiftool-13.27_64' file

	- In this file is an application file called exiftool (-k)

![image](https://github.com/user-attachments/assets/3eac11b5-d506-430c-8379-a736444ec651)

	- I need to copy this file to the VM's program files on the C drive in a new folder called 'ExifTool'

![image](https://github.com/user-attachments/assets/6d36c192-478f-45c3-ae5f-660ee5f88cc8)

	- Then I'll just rename this file to just 'exiftool'

![image](https://github.com/user-attachments/assets/02a978df-8d4d-4df0-a9ad-fdb88e8764ca)

	- Now I need to copy the file path at the top file path bar

	- Then I need to open 'Run' application

![image](https://github.com/user-attachments/assets/ec590bc8-1a10-4d1f-a0ab-5f93f75d61bf)

	- I then need to type "SystemPropertiesAdvanced"

![image](https://github.com/user-attachments/assets/dd15943b-bc0d-4603-b2ae-1429e537d7d1)

	- This will bring up the System Properties window

![image](https://github.com/user-attachments/assets/ec51205f-d4c9-47b4-9eaa-5e276c1f14e2)

	- I need to select "Environment Variables" at the bottom of the window
		○ This will bring up the environmental variables window
		○ I can see user variables 
		○ I can also see system variables

	- Environmental variables are key-value pairs that tell the system or programs how to behave. They store info like file paths, settings, and user/session data.
		○ They essentially help programs find things (like there Python or Java is installed)
		○ They also control behavior (like temp fiel location, language, etc.)

	- Environmental variables:
		○ Let apps run properly
		○ Help scripts and software find needed resources
		○ Useful for automation and development

	- User variables:
		○ Only apply to the current user (e.g. your profile's PATH)

	- System variables:
		○ Apply to all users on the computer (set by the admin or the OS)

	- Under "System Variables", I'll need to select the "Path" option


![image](https://github.com/user-attachments/assets/14e450b7-6de0-477d-b5f6-dca02c4ca752)

	- Once selected I'll need to select the "Edit" option at the bottom
		○ This will bring up the "Edit environment variable" window

![image](https://github.com/user-attachments/assets/b0cc9020-c315-4e46-b59d-353a6f773c7a)

	-  I need to select "New" at the top, and then paste in the ExifTool folder path

	- So what did this do?

	- Well ExifTool is a command-line tool, so to use it from any folder in Command Prompt or PowerShell, Windows needs to know where to find it.
		○ By adding the ExifTool folder to the System 'Path' variable, I'm telling Windows:
		○ "Hey, the folder has a program I want to use from anywhere"
		○ That way, I can just type "exiftool" in Command Prompt without having to be in its exact folder every time.

	- I can now use ExifTool as I please!


P.S. 

 - For some reason it was not running in command prompt but thanks to the helpful youtube comment below, it now works.

![image](https://github.com/user-attachments/assets/f34d1735-62f1-40e8-a426-81c7ec65c93e)

![image](https://github.com/user-attachments/assets/bdfa52f5-1e58-4e97-837f-344106253548)

	- Now let's start the actual lab


