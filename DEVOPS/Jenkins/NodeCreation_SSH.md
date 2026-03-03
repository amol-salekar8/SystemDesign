# Node Creation and Connection Using SSH

#### How we connect master and slave
1) With the help of ssh we are connecting nodes
2) Using public and private key
3) Generate key with following command
    - Go to this folder
   ``` Bash
      cd ~/.ssh
   ```
    - Generate the key with below command
   ``` Bash
   ssh-keygen
   ```
![](./image/creationOfPublicAndPrivateKey.png)
4) Go to Manage_Jenkins/Nodes
    - Name : (give name) (i.e. Agent_Vinod)
    - Remote root directory : (path where you perform an operation) (i.e. /home/ubuntu )
    - Labels : (IMP part) (i.e. Vinod)
    - Launch Method : (We are connecting with the help SSH)
      ![](./image/node_launchMethod.png)
        - Host :  add node IP address to that
   ``` BASH
   
   ubuntu@ip-172-31-4-203: ~/.ssh$ ls
   authorized_keys  id_ed25519  id_ed25519.pub
   ubuntu@ip-172-31-4-203: ~/.ssh$ cat ^C
   ubuntu@ip-172-31-4-203: ~/.ssh$ cat id_ed25519
   -----BEGIN OPENSSH PRIVATE KEY-----
   b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
   QyNTUxOQAAACCXXXBOVLvQGBD9qKJPlHjEyx7dY/MRVjn9TwV6LtZ9QwAAAKBC7KBdQuyg
   XQAAAAtzc2gtZWQyNTUxOQAAACCXXXBOVLvQGBD9qKJPlHjEyx7dY/MRVjn9TwV6LtZ9Qw
   AAAEBS/MK2JcWeaWK1Cn4xh+Uqp589voyZjKb7so07Mht2R5ddcE5Uu9AYEP2ook+UeMTL
   Ht1j8xFWOf1PBXou1n1DAAAAFnVidW50dUBpcC0xNzItMzEtNC0yMDMBAgMEBQYH
   -----END OPENSSH PRIVATE KEY-----
   
   ```
    - Credentials : click on add -> Add SSH Username with private key
      ![](./image/addMasterPrivateKeyToNode.png)
    - ID : give name for SSH
    - Username : system name of master (should be correct name)
    - Private key : we are adding master private key in the node
    - After complete the above step click on create
5) After completing all the steps click on save
6) If you didn't add master public key to the agent node to the following path  ~/.ssh/authorized_keys then it can't established connection.
7) Add node to the pipeline
![addNodeToThePipeLine.png](./image/addNodeToThePipeLine.png)
