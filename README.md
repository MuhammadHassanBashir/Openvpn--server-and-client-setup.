# Openvpn-server-and-client-setup.

## openvpn setup link

https://github.com/AliBigdeli/OpenVPN-Server-Setup#step-3-create-user     ----github link to setup openvpn remote server on any server

## After successfully setting up openvpn. You will find 1 folder and 1 file named below in the same directory..

        1- OpenVpn  
        2- openvpn-install.sh

## Now its time to add users(profiles)  to openvpn server. Use below commands for this

        chmod +x openvpn-install.sh
        sudo ./openvpn-install.sh

  After executing **./openvpn-install.sh** you will see the option like this.. follow steps one by one...   

          Welcome to OpenVPN-install!
          The git repository is available at: https://github.com/angristan/openvpn-install
          
          It looks like OpenVPN is already installed.
          
          What do you want to do?
             1) Add a new user
             2) Revoke existing user
             3) Remove OpenVPN
             4) Exit
          Select an option [1-4]: 1            -------------------------------------------------------> for adding new user to openvpn server
          Tell me a name for the client.
          The name must consist of alphanumeric character. It may also include an underscore or a dash.
          Client name: fakher            -------------------------------------------------------------> give the same of user and enter
          
          Do you want to protect the configuration file with a password?
          (e.g. encrypt the private key with a password)
             1) Add a passwordless client
             2) Use a password for the client
          Select an option [1-2]: 2    -----------------------------------------------------------------> select for setting up users password
            ⚠️ You will be asked for the client password below ⚠️
          
          * Using SSL: openssl OpenSSL 3.0.2 15 Mar 2022 (Library: OpenSSL 3.0.2 15 Mar 2022)
          
          * Using Easy-RSA configuration: /etc/openvpn/easy-rsa/vars
          
          * The preferred location for 'vars' is within the PKI folder.
            To silence this message move your 'vars' file to your PKI
            or declare your 'vars' file with option: --vars=<FILE>
          Enter PEM pass phrase:                           ------------------------------------------------> set user password
          Verifying - Enter PEM pass phrase:                ------------------------------------------------> verify user password
        
        After that it will give you the below information 
            
            Notice
            ------
            Keypair and certificate request completed. Your files are:
            req: /etc/openvpn/easy-rsa/pki/reqs/fakher.req
            key: /etc/openvpn/easy-rsa/pki/private/fakher.key
            Using configuration from /etc/openvpn/easy-rsa/pki/2cf0ec43/temp.ce6edbb7
            Check that the request matches the signature
            Signature ok
            The Subject's Distinguished Name is as follows
            commonName            :ASN.1 12:'fakher'                         ---------------> name of the user added in openvpn server
            Certificate is to be certified until Sep 10 14:30:16 2034 GMT (3650 days)
            
            Write out database with 1 new entries
            Data Base Updated
            
            Notice
            ------
            Certificate created at:
            * /etc/openvpn/easy-rsa/pki/issued/fakher.crt
            
            Notice
            ------
            Inline file created:
            * /etc/openvpn/easy-rsa/pki/inline/fakher.inline
            Client fakher added.
            
            The configuration file has been written to /root/fakher.ovpn.  ----------------------------> path of .ovpn file that need to share to the user, So user can use this and connect openvpn server from local system. you can **cat the .ovpn file from the path and with this make .ovpn file having same name on to your system and send this file to user** or you can use **scp or rsync command for downloading it from remote server to you localsystem**.                 
            Download the .ovpn file and import it in your OpenVPN client.

        remember to switch the root user with **sudo su** because other user have no right to go to the /root/file.ovpn file and read the file...

## How to connect from local system to openvpn server by using .ovpn file

### FOR LINUX Install OpenVPN client into your local (if it's not already installed):

          sudo apt update
          sudo apt install openvpn

Start OpenVPN with a configuration file: You need an .ovpn configuration file to connect to a VPN. You can start OpenVPN using this file with the following command:

          sudo openvpn --config /path/to/your-vpn-config-file.ovpn

  Like 

          sudo openvpn --config /home/hassan/fakher.ovpn 

### For window install openvpn software in windows system. and add .ovpn client file(profile) that got from the admin like "fakher.ovpn" in my case in openvpn client software import profiles section.. it will connect openvpn client to openvpn remote server..


## Verfication

  Go to the browser and brows what is my ip.. And you will get ip address of open vpn remote server...
