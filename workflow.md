# Raspberry Pi workflow

## SSH into Raspberry Pi from Mac
* Find the IP address of the Raspberry Pi device 
```shell
~ hostname -I
// 192.168.1.12 
```
* Reset the password. Open the Pi with a monitor, keyboard and mouse. 

  Click on Preferences > Rasbperry Pi Configuration > Password: Change Password

  Remember the password

* From the Mac terminal ssh into Pi `sssh pi@<pi-ip-address>` and enter the set password
```shell
~ ssh pi@192.168.1.12
pi@192.168.1.12's password:
```

## Access Pi files from VSCode on Mac
* This is only possible because of setup steps below
1. Run the following command within VSCode Editor
```shell
~ ssh pi3
pi@192.168.1.12's password:
```
2. Once login and ssh successful into pi look for the file you would like to open and run the command
```shell
~ rmate <file>
```

## Use VSCode to edit Rasbperry Pi files
* Visit the [following guide](https://blog.technologee.co.uk/remote-editing-using-vs-code/) to install RemoteVSCode extension on VSCode and rmate on the Pi device
* Once installed, open VSCode editor and ⇧⌘P and then look for: Remote: Start Server
* Run the following command within VSCode terminal `ssh -R 52698:127.0.0.1:52698 pi@<pi-ip-address>`
* Follow the same ssh login steps as above
* Then with the server running locally within VS Code we can call  `rmate <file>` on the Pi and the file will open within VS Code.

## Further refinement
* Adding the ssh tunnel element to the command when initiating the connection may be cumbersome and become difficult to remember. Fortunately, through the use of a `~/.ssh/config` file we can ensure that the tunnel is configured every time we create a connection to our Pi.

```
Host pi3  
    HostName <pi-ip-address>
    User pi
    ForwardAgent yes
    RemoteForward 52698 127.0.0.1:52698
```
* Now, once we have started the server within VS Code, all we need to run is `ssh pi3` and the resulting connection will have our ssh tunnel automatically configured.