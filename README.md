# sshBruteforcer
SSH provides the means to authenticate using public key cryptography. In this scenario, the server knows the public key and
the user knows the private key. Using either RSA or DSA algorithms, the server produces these keys for logging into SSH. 
Typically, this provides an excellent method for authentication. 

With the ability to generate 1024-bit, 2048-bit, or 4096-bit keys, this authentication process makes it difficult to use brute force
as we did with weak passwords. It would be nice if we could build a tool to exploit this vulnerability. However, with access to the 
key space, it is possible to write a small Python script to brute force through each of the 32,767 keys in order to authenticate to a 
passwordless SSH server that relies upon a public-key cryptograph.

To authenticate to SSH with a key, we need to type [ssh user@host –i keyfile –o PasswordAuthentication=no]. For the following script,
we loop through the set of generated keys and attempt a connection. If the connection succeeds, we print the name of the keyfile to 
the screen. Additionally, we will use two global variables Stop and Fails. 

Fails will keep count of the number of failed connection we have had due to the remote host closing the connection. If this number is 
greater than 5, we will terminate our script. If our scan has triggered a remote IPS that prevents our connection, there is no sense
continuing. 

Our Stop global variable is a Boolean that lets us known that we have a found a key and the main() function does not need to start 
any new connection threads. 
