## Access Guide for BIO5025

## Required Software
### SSH Client
•	Windows Users: Install MobaXterm (recommended).

Download [MobaXterm](https://mobaxterm.mobatek.net/)

•	Mac/Linux Users: Use the built-in Terminal (no additional installation required).


## 1.) Connecting to the Server

## Using SSH client:

–	Windows: Open MobaXterm and start a new SSH session.

–	Mac/Linux: Open Terminal.

### 1.1.) Run the following command:

```console
ssh USERNAME@52.138.157.130
```

Enter your password when prompted.
   
## 2-) Transfering Files

### 2.1.) Using SCP (Mac/Linux)

To upload a file from your computer to the server:
```console
scp myfile.txt USERNAME@52.138.157.130:~/
```

To download a file from the server to your computer:

```console
scp USERNAME@52.138.157.130:~/myfile.txt ./
````

### 2.2.) Using FileZilla

### FTP Client
To transfer files between your local machine and the server:

•	Recommended: [FileZilla Client](https://filezilla-project.org/) 

•	Any SFTP-compatible client is also fine.

1.	Open FileZilla.
2.	Go to Site Manager → Create a new site.
3.	Enter the following details:
   
–	Protocol: SFTP

–	Host: 52.138.157.130

–	Logon Type: Normal

–	User: Your username

–	Password: Your password

5.	Click Connect to access your server files.

The file portion of this other tutorial might be helpful for you: https://eukaryotic-genome-assembly.github.io/logging_on/ 
