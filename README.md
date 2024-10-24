<h1>Algorithm for file updates in Python</h1>


<h2>Description</h2>
Project Scenario: <br/>
I'm a security analyst working at a healthcare company. At my organization, access to restricted data containing PHI is controlled with an allow list of IP addresses. I'm required to regularly update a file that identifies the employees who are authorized to access restricted data. The contents of the file are based on who is working with sensitive patient records. Employees are restricted access based on their IP address. There is an allow list for IP addresses permitted to sign into the restricted subnetwork. There's also a remove list that identifies which employees I must remove from this allow list.<br/><br/>
My task is to create an algorithm that uses Python code to check whether the allow list contains any IP addresses identified on the remove list. If so, I should remove those IP addresses from the file containing the allow list.<br/>

<br />


<h2>Languages and Utilities Used</h2>

- <b>Pyhton</b> 

<h2>Environments Used </h2>

- <b>Mac OS</b> (15.xx version)

<h2>Program walk-through:</h2>

<p align="center">
  <b>Open the file that contains the allow list</b></p>  <br/>
The following code demonstrates how I used Linux commands to determine the existing permissions set for a specific directory in the file system. <br/><br/>
<img src="https://i.imghippo.com/files/KEW4013KJk.png"height="80%" width="80%" alt=""/>
The first line of the screenshot displays the command I entered, and the other lines display the output. The code lists all contents of the projects directory. I used the ls command with the -la option to display a detailed listing of the file contents that also returned hidden files. The output of my command indicates that there is one directory named drafts, one hidden file named .project_x.txt, and five other project files. The 10-character string in the first column represents the permissions set on each file or directory.
<br />
<br />
<p align="center"><b>Describe the permissions string</b>  <br/></p>
The 10-character string can be deconstructed to determine who is authorized to access the file and their specific permissions. The characters and what they represent are as follows:<br/>
- 1st character: This character is either a d or hyphen (-) and indicates the file type. If it’s a d, it’s a directory. If it’s a hyphen (-), it’s a regular file.<br/>
- 2nd-4th characters: These characters indicate the read (r), write (w), and execute (x) permissions for the user. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted to the user.<br/>
- 5th-7th characters: These characters indicate the read (r), write (w), and execute (x) permissions for the group. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted for the group.<br/>
- 8th-10th characters: These characters indicate the read (r), write (w), and execute (x) permissions for other. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen (-) instead, that indicates that this permission is not granted for other.
<br />
<br />
<p align="center">
  <b>Change File Permissions</b></p>  <br/>
The organization determined that other shouldn't have write access to any of their files. To comply with this, I referred to the file permissions that I previously returned. I determined project_k.txt must have the write access removed for other.<br/>
<br/>

The following code demonstrates how I used Linux commands to do this:<br/>

<img src="https://i.imghippo.com/files/iVsmE1729471023.png" height="60%" width="60%" alt=""/>

The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. The chmod command changes the permissions on files and directories. The first argument indicates what permissions should be changed, and the second argument specifies the file or directory. In this example, I removed write permissions from other for the project_k.txt file. After this, I used ls -la to review the updates I made.<br/>
<br/>

<p align="center">
  <b>Change file permissions on a hidden file</b></p>  <br/>
The research team at my organization recently archived project_x.txt. They do not want anyone to have write access to this project, but the user and group should have read access. <br/>
<br/<

The following code demonstrates how I used Linux commands to change the permissions:<br/>

<img src="https://i.imghippo.com/files/ImMnT1729471344.png" height="60%" width="60%" alt=""/>
The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. I know .project_x.txt is a hidden file because it starts with a period (.). In this example, I removed write permissions from the user and group, and added read permissions to the group. I removed write permissions from the user with u-w. Then, I removed write permissions from the group with g-w, and added read permissions to the group with g+r. 
<br />
<br />
<p align="center">
  <b>Change directory permissions</b></p>  <br/>
My organization only wants the researcher2 user to have access to the drafts directory and its contents. This means that no one other than researcher2 should have execute permissions.<br/>
<br/>
The following code demonstrates how I used Linux commands to change the permissions:<br/>

<img src="https://i.imghippo.com/files/paBbB1729471466.png" height="60%" width="60%" alt=""/>
The output here displays the permission listing for several files and directories. Line 1 indicates the current directory (projects), and line 2 indicates the parent directory (home). Line 3 indicates a regular file titled .project_x.txt. Line 4 is the directory (drafts) with restricted permissions. Here you can see that only researcher2 has execute permissions.  It was previously determined that the group had execute permissions, so I used the chmod command to remove them. The researcher2 user already had execute permissions, so they did not need to be added.
<br />
<br />
<p align="center">
  <b>Summary</b></p>  <br/>

I changed multiple permissions to match the level of authorization my organization wanted for files and directories in the projects directory. The first step in this was using ls -la to check the permissions for the directory. This informed my decisions in the following steps. I then used the chmod command multiple times to change the permissions on files and directories.

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>


