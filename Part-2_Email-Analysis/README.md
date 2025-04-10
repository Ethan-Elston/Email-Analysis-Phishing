# Performing email analysis

## Steps

	- Email analysis:
		○ It involves examining an email's components to detect threats such as phishing, malware, spoofing, or spam

	- Analysts look at:
		○ Headers:
			§ To trace sender, checking spoofing, and analyze routing
		○ Body:
			§ To find suspicious language, requests, or formatting
		○ Attachments:
			§ To scan for malware, executables, or scripts
		○ Links/URLs:
			§ To check if they redirect to malicious or fake websites

	- Purpose:
		○ To identify and stop email-based attacks before they compromise users or systems

	- Phishing:
		○ When an attacker tricks someone into giving up sensitive information (like passwords, or credit card numbers) by pretending to be a trusted source. It's usually done through fake emails, websites, or messages, that look real but are designed to steal data.



Lab:

	- I'll be doing CTF like lab on blueteamlabs.online  called "The Planet's Prestige"

	- Scenario is below:

![image](https://github.com/user-attachments/assets/db765dbf-58d2-4b02-b142-64a4205a9181)

	- I'm guessing this email is what  I will be looking through
		○ I need to go ahead and download it
		○ Then extract the zip file.

	- After I enter the password, I can see a 'EML File' named a "A Hope to CoCanDa"

	- EML File:
		○ A email file format that stores the full email content (subject, body, attachments), and the headers (sender, recipient, timestamps, etc.)

![image](https://github.com/user-attachments/assets/1e1d0698-c78e-47ed-983a-240370264a08)

	- I'll be using Notepad++ to perform analysis on this email file.

	- I'll need to right-click the file and select the "Edit with Notepad++" option

![image](https://github.com/user-attachments/assets/8629ffee-7cf8-4f2f-819c-ab7243a013a8)

![image](https://github.com/user-attachments/assets/6634cf62-1aa9-45dc-9592-169f9bc2c46a)

	- As you can see above, clicking this option displays the EML file in Notepad++. There is a ton of information here.  I'd be lying if I said I'm not a little bit intimidated

	- To start dissecting the data, I'll need to take a look at the fields.

	- The very first field is the "Delivered-To" field. 
		○ This shows who received the email. In this case the email address "themajoronearth@gmail.com"

![image](https://github.com/user-attachments/assets/3e88898d-0635-48d4-817e-8d2dfb3b426d)

	- The second field is a "Received" field. 
		○ There is a reason I used "a". There are multiple "Received" fields
		○ These are emails servers that have received the email

	- The email will end up in multiple email servers before it ends up in the email server that is closest to the recipient 

	- The top "Received" field of the EML file is the closest mail server to the recipient

![image](https://github.com/user-attachments/assets/e27fa3e2-5050-4165-9f34-e996e3c1fd6d)

	- If I scroll down further I can find the first "Received" field

 ![image](https://github.com/user-attachments/assets/f5fe94c4-33f6-475c-a321-cc307c4f744e)

		- This mail server is the one closest to the sender


	- Top Received Field: 
		○ Closest mail server to the recipient 
	- Bottom Received Field:
		○ Closest mail server to the sender 


	- Let's look at the next fields:

![image](https://github.com/user-attachments/assets/cdcc5a68-0532-48fb-aa1a-6b588aa616b9)

	- The next fields are headers that have an X appended to the front 
		○ "X-Google-Smtp-Source"
		○ "X-Received"

	- These are called "X headers"
		○ Optional
		○ Included by tools or mail servers

	- Next is a handful of "ARC" headers
		○ ARC stands for "authenticated received chain headers"
		○ These are used for verifications purposes by having a trusted intermediate email server sign the header 

	- Next is the "Return-Path" field

![image](https://github.com/user-attachments/assets/4d7940e5-d9db-4cbe-a866-1d0603c71e81)

	- This is the email address that will be used if the email fails to send  
		○ Frequently used for troubleshooting purposes

	- The next important field is "Authentication-Results"

![image](https://github.com/user-attachments/assets/b7581be0-d0c1-4857-baf8-185610bb3347)

	- Here we can see the statuses for email protection. This includes:
		○ SPF
		○ DKIM
		○ DMARC

	- As you can see, SPF is set to fail. This means that the domain "microapple.com" does not permit the mail server with an IP address of 93.99.104.210 as a permitted sender 
		○ Essentially microapple.com has no idea who 93.99.104.210 is 

	- When performing email analysis, looking at the SPF, DKIM, and DMARC statuses is a good indicator for suspicious emails. 
		○ For instance, if SPF is set to fail, you should take definitely take a deeper look 

	- "To", "Subject", "From" fields:

![image](https://github.com/user-attachments/assets/d2a2d13f-054d-468e-8b63-d4e7cea29573)

	- The "To" field shows the recipient

	- The "Subject" field shows the subject of the email

	- The "From" field shows who sent the email
		○ This is important in email analysis, I need to take note of this


	- If I scroll down just a bit, I can see the "Reply-To" field

![image](https://github.com/user-attachments/assets/0c738727-d548-4fa0-881f-a9d9599d1f69)

	- The email address in this field is what would be used the moment the recipient clicks on 'reply' to the email   
		○ The domain is "pashter.com"

	- This is very important, and I need to take note of this

	- This is different than the domain "microapple.com" in the "From" field
		○ This is very suspicious, they should be the same

	- So now I know that the SPF failed, and there are two different email addresses in the "From" and "Reply-To" fields


	- Moving on, I can see a couple more fields. Take a look at the 3 below:

![image](https://github.com/user-attachments/assets/d35646b2-1aa1-4c2c-8674-a8bb8a909610)

	- "Content-Type" field
		○ This fields instructs the mail server on how to render the content of the email.
		○ "multipart/mixed" means there are multiple formats
		○ There is also a boundary set
		○ A boundary is used to let the mail server know when to start and stop rendering using a certain format

	- "Message-Id" field
		○ A unique identifier to help keep track of this particular email   

	- "Date" field
		○ This is when the recipient received the email
		○ NOTE that this field can be spoofed 


	- After these fields, I can see the first boundary of the email

![image](https://github.com/user-attachments/assets/5543a334-88b3-435e-8c5c-b290c865e4bb)

	- As you can see it's the same value that was set in the "Content-Type" field

	- This will tell the mail server to start rendering the content using the following format
		○ The 'Content-Type' is 'text/plain'
		○ This is telling the mail server "hey render this content using plain text format"
		○ However the 'Content-Transfer-Encoding' is set to 'base64'
		○ So this is also telling the mail server "hey encode the plain text using base64 as well"

	- The content is then shown below encoded in base64, I need to use the browser tool CyberChef to decode it and view the contents
		○ I'll just copy and paste it into the CyberChef input

![image](https://github.com/user-attachments/assets/339796d0-119e-4f13-b9c2-45c9d9a086e3)

	- Then on the left, I'll need to select the 'From Base64' option and drag it over to under the 'Recipe' portion

	- After I do this, it's automatically decoded, and I can view the output

![image](https://github.com/user-attachments/assets/4ba34c29-9b7c-4ff1-8f03-87b42163cc9d)

	- So this is very important, and I'll need to save this output to a file for potential future use.
		○ To do this, I need to click the save button at the top
		○ I'll then name the file, "email.txt"

![image](https://github.com/user-attachments/assets/1957105e-7109-4356-b2ba-923792618117)

	- So the kidnappers mentioned an attachment 

	- To find this, I'll need to go back to Notepad++
		○ If I scroll down, I can see the second boundary in this email
		○ This tells the mail server that this is the end for that particular piece of content
		○ Then the new fields below that are instructing the mail server how to format the following content again

![image](https://github.com/user-attachments/assets/89898f34-3a5c-4308-97be-cf6b54bab39f)

	- The 'Content-Type' now has 'application/pdf' with the name 'PuzzleToCoCanDa.pdf'
		○ So this is the attachment that was mentioned in the body of the email

	- 'Content-Transfer-Encoding' is set to base64, so the content will be encoded with base64

	- I'll need to do the same as last time, and copy all of the encoded content into CyberChef

![image](https://github.com/user-attachments/assets/3ba2973f-3aae-4387-8096-72feddb27dc9)

	- Now I can add multiple operations to the "Recipe"

	- I'm going to drag over the 'To Hex' operation into the Recipe portion as well
		○ This will convert the content into hexadecimal

![image](https://github.com/user-attachments/assets/648723a4-2414-48f7-ba92-b148a9823393)

	- So why convert this into hexadecimal?

	- I wanted to know what the first couple of bytes were. In this case they were:
		○ 50
		○ 4b
		○ 03
		○ 04

	- The first bytes of a file makes up what is called a 'file signature'

	- A file signature (also called a magic number) is a unique set of bytes at the start of a file that identifies its file type, regardless of its file extension. 
		○ This helps detect file spoofing (e.g., .jpg file that’s actually a .exe file)
		○ Used in malware analysis and digital forensics to verify the file types

	- So even though the file is named "PuzzleToCoCanDa.pdf", it doesn't necessarily mean it's a .pdf file

	- You always want to look at the file signature of a file to determine exactly what that file is

	- To find out more about what the file actually is, I'll copy the file signature and use a website/tool called "GaryKessler File Signatures"

![image](https://github.com/user-attachments/assets/7205a4a3-1d04-4edd-b8ba-dc455d428e71)

	- Then once on the site, I just need to use "ctrl + f" and paste in those first couple of bytes

![image](https://github.com/user-attachments/assets/4e2b14aa-e47d-4e48-9da0-ed3a17188965)

	- So I can see that these bytes relate to a zip extension
		○ This is very interesting 

	- So the in the file name it had an extension of .pdf but here we can clearly see that it's real file extension is .zip

	- So what is the file signature of a .pdf file? Well I just type pdf into the find bar 

![image](https://github.com/user-attachments/assets/9b6bb9ae-6dfd-4f0c-b306-423053caeb52)

	- Here I can clearly see that the first couple of bytes for a pdf extension is '25 50 44 46'
		○ This is not the same as the first couple of bytes in our ".pdf" file

![image](https://github.com/user-attachments/assets/992dd94f-b297-4e27-a5dd-5ad36484ad1f)


	- Now that I know the file signature, and the real file type, I can go back to CyberChef and remove the 'To Hex' operation and save the decoded base64 output to a file
		○ I'll name this file 'ATTACHMENT.ZIP'

![image](https://github.com/user-attachments/assets/481e2f8c-558f-4582-80b1-3c346f5466d9)

	- I'll head over to file explorer, right-click this file, and then select "Extract-All"

![image](https://github.com/user-attachments/assets/4fbb7032-aa31-4348-8862-e1b26551afe0)

	- In it is a "PuzzleToCoCanDa" directory 

	- When opened, I can see two files 
		○ "DaughtersCrown"
		○ "GoodJobMajor"

![image](https://github.com/user-attachments/assets/f7485187-28f2-4643-897b-1e6ebc8dc895)

	- It's always good practice to check for hidden files before you start to mess around and make sure you can view file name extensions
		○ To do this I'll need to click "View" at the top
		○ Then check the "Hidden items" box 
		○ And the file name extensions box

![image](https://github.com/user-attachments/assets/3de3c9a8-e8d6-432d-b8de-ac6e47c02477)

	- I can now see a new file called "Money.xlsx"!!!
		○ '.xlsx' is a file extension for Microsoft excel 

![image](https://github.com/user-attachments/assets/2a635f3d-3ba4-4c12-b00f-0dfb11ba9931)

	- So does this file really have an excel file extension?


	- This is where the tool HxD comes into play
		○ I can view these files in their Hex format using this tool

	- I'll need to open the HxD tool, and then I can drag the files from file explorer into HxD
		○ I'll start with the file "DaughtersCrown"

![image](https://github.com/user-attachments/assets/9ae35b0a-7162-472a-b843-14862cfbf806)

	- The first couple of bytes is:
		○ FF
		○ D8
		○ FF
		○ E0

	- Then I'll copy these and head over to GaryKessler File Signatures, and paste that into the find box

 ![image](https://github.com/user-attachments/assets/b2f9e82a-2a96-4a90-9914-1826bab87049)

	- I can see that these bytes relate to a JPEG file

	- A good practice is to go back and rename the file once you've figured out the real file type. This helps you remember the file, helps you stay aware of potential danger, etc. 
		○ Just right-click the file, and the select the 'Rename' option

![image](https://github.com/user-attachments/assets/f069e7c9-b86e-445d-8433-348df8411f39)

	- Now time to open it. 

![image](https://github.com/user-attachments/assets/0d8a1930-bb03-4b60-aaab-e52a86b7975a)

	- A picture of a crown…

	- Let's move on to the 'GoodJobMajor' file
		○ I'll follow the same steps

	- However I'll need to click "New" in HxD

![image](https://github.com/user-attachments/assets/b493d353-b329-43c2-8165-eb895d4a5bd2)

	- Then I need to drag the file into HxD
		○ Here is the file in HxD below. 

![image](https://github.com/user-attachments/assets/c848b220-3bd7-4a89-99e4-8e84520d7565)

	- First bytes:
		○ 25
		○ 50
		○ 44
		○ 46

	- Are these numbers familiar? These are the same bytes that are associated with a PDF file that I saw earlier
		○ Now I'll go back and give the file a .pdf file extension

![image](https://github.com/user-attachments/assets/192b52dd-36ad-43d3-a049-38ba17ffa1cd)

	- Now let's open it.
		○ It opens the following in my browser.
  
![image](https://github.com/user-attachments/assets/2d84fc75-e0f4-412b-b05e-635a4c046605)

	- Now it's time to open 'Money.xlsx' in HxD

![image](https://github.com/user-attachments/assets/831a6d49-8e3f-4f07-9655-f72921c589be)

	- First bytes:
		○ 50
		○ 4B
		○ 03
		○ 04

	- Now I need to go search for this in GaryKessler File Signatures
		○ This is the same bytes as earlier, so I know that it can be associated with a zip file, but I do remember there were a couple more files that these bytes could be associated with

	- If I scroll down just a bit, I can see that it is also associated with Microsoft Office Open XML format (excel)

![image](https://github.com/user-attachments/assets/59db4889-4825-4bc0-a8a9-eb7f8699b559)

	- So this is a legit excel document


	- I don't want to go through the hassle of downloading the Excel application on my VM in the middle of my lab. 
		○ I can use a browser based tool called SquareX to view the excel file

	- SquareX is a browser security tool that offers:
		○ Disposable browsers: 
			§ Opens links safely in a cloud session, isolated from your device
		○ Disposable file viewers:
			§ View risky files without downloading them
		○ Disposable emails
			§ Use temporary emails to avoid spam/phishing 

	- I'll be using their disposable file viewer, so that I can drag and drop the excel file and view its contents
	
![image](https://github.com/user-attachments/assets/f703bd3a-1e5d-480b-a38e-7e2f9ec6ab21)

	- I have it as a browser extension, and once I logged in I had access to the file viewer below

![image](https://github.com/user-attachments/assets/45b66fed-8576-4aac-b95f-ed41c73523c9)

	- So now I'll just drag and drop the .xlsx file

![image](https://github.com/user-attachments/assets/bebf79ef-cdc1-4d5f-9a1a-76600b0c190c)

	- I looked at Sheet3 as well, it had nothing in it

	- Remember that this lab is CTF-like so there might be some hidden text or something of the sort, I'm not seeing. 

	- For instance there could be text that is blended into the background using the color white. To check, I'll do the following. 
		○ I'll select everything using 'Ctrl + A'
		○ Then I'll select 'Clear' and then 'Format'

![image](https://github.com/user-attachments/assets/759f3d8f-bc9a-4d1a-ae43-99da3baa9769)

	- This way if there is any kind of formatting that's happening, I will see it 

	- What about Sheet3 though?
		○ I'll select everything
		○ Then clear the format

![image](https://github.com/user-attachments/assets/d993d117-c612-4bc5-971e-bcd118ded8ac)

	- Of course there is a hidden base64
		○ Indicated by the "==" at the end of the string
		○ I'll copy this and decode it in CyberChef

![image](https://github.com/user-attachments/assets/55089f41-211a-4c9e-9fe0-80060054b080)

	- Interesting. "The Martian Colony, Beside Interplanetary Spaceport."

Ending Notes:

Malicious actor sent an email from:
		○ billjobs@microapple.com
To the email:
		○ Themajoronearth@gmail.com
With a subject of:
		○ A Hope to CoCanDa
On the date:
		○ January 26th, 2021 at 01L41:18 EST
	

The Return-Path is:
		○ billjobs@microapple.com
		○ This email will receive any emails that failed to deliver
	
The Reply-To however is a completely different email:
		○ negeja3921@pashter.com

The malicious actor used an email service called 'emkei.cz'
		○ This is a fake mailer
		○ A quick search of this on Google shows that this is a fake mailer

![image](https://github.com/user-attachments/assets/5fd2b4d3-4412-45b2-ada1-94b0eedd2f68)

![image](https://github.com/user-attachments/assets/93ddbabe-86f8-4372-8378-18232a15131d)

The contents involved a threat to the major on earth, demanding 1 billion in cash

There was also an .pdf attachment that was secretly a .zip file
		○ Within this .zip file were 3 files
		○ 1 .jpeg file
		○ 1 .pdf file
		○ 1 excel file
	
	- When performing email analysis there are some important fields that you should put more focus on. They are listed below:
		○ "Received" field
			§ Mail servers that received the email
			§ Perform OSINT on these email servers 
			§ Look at the IP reputation and domain reputation as well
			§ Also perform OSINT on the email service
		○ "Return-Path"
			§ Look at the email address itself 
			§ Remember that the return-path is the email address that will receive a failed or error in email delivery
		○ "Authentication-Results"
			§ You can find the status of SPF, DKIM, DMARC
			§ If any of these are set to failed, it's probably worth investigating the email
		○ "To"
			§ This is the recipient who received the email
		○ "Subject"
			§ This is important if you have an email security Gateway or if you have the ability to search emails across your organization
			§ You can use the subject field to see who else received a similar email
		○ "From"
			§ Who sent the email
			§ Focus on the email address itself
		○ "Reply-To"
			§ The email address that will be used if the recipient clicks on reply
			§ You can get a "quick-win" if you notice that the "From" email address and the "Reply-To" email address are different 
			§ If someone sends an email, they should be the ones getting the reply as well
		○ "Content-Type"
			§ How the mail server renders the content of the email
			§ If you see "boundary", that means you can see multiple formats of the content in the email
		○ "Message-Id"
			§ This is very useful is you're searching emails across the organization 
			§ Keeps track of where the email went
		○ "Date"
			§ Can be spoofed
			§ But still need to take note of it 

	- Any time I received an email, I need to focus on these fields.



Answers to Questions:

![image](https://github.com/user-attachments/assets/003e2d41-d770-4044-92cd-40cd41b8b51b)

	- The question: "What is the name of the malicious actor?" is a little tricky
		○ It says I need a first AND last name…
		○ In the "From" field is says "Bill". This is likely spoofed, and I know that the Reply-To email address, is much more likely to be connected to the real-attacker. 

	- This is where I will use the Exif-Tool I installed earlier.
		○ I want to look at the meta-data of the attachment itself, because if the threat-actor is responsible for creating it. They very well could of left some clues for me.

	-  To use Exif-Tool, I'll need to open PowerShell and use the command
		○ Since I added the ExifTool file path to the system Path environmental variables, I can just use this simple command
		○ 'exiftool {file path}'
		○ For the file path, I'll just need to copy and paste the file path for the ATTACHMENTs folder I created earlier

![image](https://github.com/user-attachments/assets/623f8a32-309d-4108-8d58-1b83bd379ee0)

	- Within this metadata I can see a "Author"
		○ The name is "Pestero Negeja"

	- So that is the first and last name of the attacker

	- And there we go! I completed the lab!
