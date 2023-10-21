# Deploying Backend Using AWS

## Steps :

- Create AWS account
- Go to EC2
- launch an instance
- Select Ubuntu as OS
- Select instance as micro for free setup
- Create a key-value pair [IMPORTANT .cer File]
- Now Launch an instance

#

## Enabling the server to open the ports as by default all ports are blocked - [Using Inbound rules]

- http by default runs on port 80
- https by default runs on port 80
- ssh by default runs on port 22

# setUp AWS

## Commands

- To SSH into the AWS machine from the local machine

  - ssh -i <Name_Of_File.cerFile> ubuntu@ec2 url - [-i -> specify the identity file (private key) for authentication].

- To See the file on AWS Server

  - ls -ltr <Name_Of_File.cerFile> - [-l: This option (long format) displays additional information about the files, such as file permission
    -t: This option sorts the files by modification time, with the newest files displayed at the top.
    -r: This option reverses the sorting order.
    ]

- Changing File permissions

  - chmod 600 <Name_Of_File.cerFile> [The first digit (6) specifies the permission for the owner (file owner can read and write the file).
    The second and third digits (both set to 0) specify no permissions for the group and others (i.e., no read, write, or execute permissions).]

  - Again ssh to the Aws machine and start the server

# Deploy using native method pre CI/CD Days

## Part - 1

- Clone Git repo to Aws machine

  - git clone <URL.git>

- run npm install Don't work - install node using

  - curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
  - nvm install node
  - npm install
  - setup pm2 on AWS machine

### To make any update

- First ssh into the Aws machine
- pull the code from github
- stop the existing process
- re-build the code
- re-run pm2

## Part - 2

- To Automate the process using script

  - make a .sh file and write the commands
  - estblish a ssh connection and then,
  - run souce ./deploy.sh command to run the .sh file

  - instead of 2 commands we can run only one command
  - ssh -t -i <Name_Of_File.cerFile> ubuntu@ec2-url "sudo bash ~/deploy.sh"

## Part-3

- Using the github workflows to automate the updation
