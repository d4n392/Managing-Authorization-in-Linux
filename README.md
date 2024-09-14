# Managing-Authorization-in-Linux

## File permissions in Linux

In this lab I managed the permissions of files within the _/home/researcher2/projects_ directory, which is owned by me, the _researcher2_ user and the _research_team_ group. The goal was to ensure that the active permissions reflected the appropriate level of authorization. Using the principle of least privilege, I restricted access where necessary.

## Skills Learned:

- Managing file and directory permissions in Linux
- Understanding and applying the principle of least privilege
- Reading and interpreting Linux file permission strings
- Modifying file and directory permissions using both symbolic and numeric notation
- Navigating hidden files and adjusting their permissions
- Implementing security policies through access control modifications

## Tools Used:

- Linux commands: _**ls -la, chmod**_
- Linux Bash shell for navigating directories and managing authorization

### Checking file and directory details

The following code demonstrates how I used Linux commands to check the existing permissions set for the projects directory.

![image](https://github.com/user-attachments/assets/c2ba60c0-7056-479d-97da-7dffcad38b16)

First I navigated to the projects directory. Then I used the ls command with the -la switch to display a detailed listing of the file contents, including any hidden files (They start with a ‘.’). The standard output of my command shows one directory named drafts(indicated in the terminal by the blue highlight), one hidden file named .project_x.txt, and four others project files. The 10-character string in the first column describes the current permissions set for each file or directory.

### Describing the permissions string

This 10-character string can be broken down to determine who is authorized to access the file and which specific permissions they have. The specific level of permissions they have are displayed in three categories: 

read(**r**) - If a file has the read permission, the user can view or open the file's contents. If a directory has the read permission, the user can list the files and      directories inside it.
  
write(**w**) - If a file has the write permission, the user can modify or delete the file. If a directory has the write permission, the user can create, delete, or rename   files and directories within it.
  
execute(**x**) - If a file has the execute permission, the user can run the file as a program or script. If a directory has the execute permission, the user can access the  contents of the directory (e.g., navigate into it using cd).

A directory having full permissions for all owner types would be **drwxrwxrwx**:

- The **1st character** indicates the file type. The d above indicates this file is a directory. When there is a hyphen(**-**) instead, it is a regular file.  
- The **2nd-4th characters** indicate the read(**r**), write(**w**), and execute(**x**) permissions for the user. When one of these characters is a hyphen(**-**) instead, it indicates that   this permission is not granted to the user.
- The **5th-7th characters** indicate the read(**r**), write(**w**), and execute(**x**) permissions for the group. When one of these characters is a hyphen(**-**) instead, it indicates that this permission is not granted for the group.
- The **8th-10th characters** indicate the read(**r**), write(**w**), and execute(**x**) permissions for others. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen(**-**) instead,that indicates that this permission is not granted for others.

For example, the file permissions for _project_r.txt_ are **-rw-rw-r--**. The first character is a hyphen(**-**), this indicates _project_r.txt_ is a file, not a directory. The second through fourth characters indicate the user has read and write, but not execute permissions. The fifth through seventh characters indicate the group has read and write, but not execute permissions. Finally the eighth through tenth characters indicate only read permissions for others. 

### Changing file permissions

The company decided that others should not have write access to any of their files. To comply, I reviewed the previous output of file permissions (**ls -la**) in the projects directory and determined that _project_k.txt_ needed the write access removed for others. The screenshot below shows the Linux commands I used to achieve this: 

![image](https://github.com/user-attachments/assets/2d97a6d7-a731-46c2-a5f4-e863c1abbc8c)

Beneath the previous output of file permissions, the first two lines display the commands I entered, and the other lines display the output of the second command. The chmod command changes the permissions on files and directories. The first argument (o-w) indicates what permissions should be changed, and the second argument specifies the file or directory. In this example, I removed write permissions from others for the project_k.txt file. Then I used ls -la to review the updates I made.

Permissions can also be represented numerically:
**r = 4**, **w = 2**, and **x = 1**.

These numbers are added together to form the permission sets. For example:

**rwx** = 4 + 2 + 1 = 7
**r-x** = 4 + 0 + 1 = 5
**r--** = 4 + 0 + 0 = 4

So, the string **rwxr-xr--** can also be represented as **754**.
In the screenshot below I used this alternative numerical argument to remove the read permissions from group for the _project_m.txt_ file:

![image](https://github.com/user-attachments/assets/b6d69a8b-0192-4059-9c20-4bc9a728945a)

The company determined they did not want the group to have read permissions for the _project_m.txt_ file. To comply with this request I input the command **chmod** with the first argument **600** indicating I want to keep read(**4**) and write(**2**) permissions for user, remove read permissions for group, and leave the other permissions set to none(**0**). With the second argument identifying the file I want to manage permissions on, in this case **_project_m.txt_**. I then used **ls -la** to review the changes I made.

### Changing file permissions on a hidden file

The research team at the company recently archived _.project_x.txt_. They do not want anyone to have write permissions for this project, however they would like for both the user and group to have read access. The code below is how I changed the permissions using the CLI in Linux:

![image](https://github.com/user-attachments/assets/d1013031-b68f-4de9-9bfc-e1bcfb59abb8)

Beneath the previous output of file permissions, the first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. I know _.project_x.txt_ is a hidden file because it starts with a period(**.**). In this example, using the **chmod** command with the first argument **440**, I gave only read permissions to the user and group, while removing write permissions from both. Leaving others with no permissions, indicated by the **0**. 

### Changing directory permissions

My company only wants the _researcher2_ user to have access to the _drafts_ directory and its contents. This means that no one other than _researcher2_ should have execute permissions. The following code demonstrates how I used Linux commands to update the permissions:

![image](https://github.com/user-attachments/assets/d4f3938a-5ed0-4cc2-9d62-18394ee917ea)

Beneath the previous output of file permissions, the first two lines of the screenshot display the bash shell commands I entered, and the other lines display the output of the second command (**ls -la**). Looking in the first column I see that the permission settings for the directory _drafts_ is **drwx--x---**. To remove the execute permissions from the group I input the **chmod** command with the **g-x** argument, and then specified the _drafts_ directory by typing **drafts** as my second argument. Since the _researcher2_ user already had execute permissions, no further changes were needed.

## Summary
Using Linux Bash shell commands I was able to manage the authorization settings for the company. Effectively using least privilege in alignment with the company’s security goals, I navigated to the appropriate _projects_ directory, examined the current file and directory permissions, changed permissions on files, including hidden files, and changed permissions on directories. 















































