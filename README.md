# Port Forwarding Setup for Deterlab

### Setup:
1. Run ```bash /share/port-forward-setup.sh``` on Deterlab. You must be in your XDC.
2. Access your ```/home/user``` directory on the left sidebar of Jupyter. The output of the script will be titled "port-forward-data.tar.gz".
3. Right-click on ```port-forward-data.tar.gz```, then click on "Download". It will download to your machine.
4. For security, delete your ```port-forward-data.tar.gz``` file from your XDC.
5. Extract ```port-forward-data.tar.gz```. You will find another tar.gz file called ```port-forward.tar.gz```. Do **NOT** extract this file. This is required for one of the three following scripts that you will run:
- port-forwarding-windows.sh
- port-forwarding-mac.sh
- port-forwarding-linux.sh
6a. Mac/Linux users: Open a terminal window and navigate to the directory where these .sh files are located. Type ```sudo ./port-forwarding-unix.sh```.
6b. Windows users: Right-click on ```port-forwarding-windows.ps1```, and click "Run with PowerShell". Once the script completes, press Enter.
7. Delete all of your extracted files when you are done. 

### How to Run:
1. To access your XDC <ins>without</ins> port-forwarding, you can type ```ssh username-xdc-proj``` in your terminal (or command prompt or PowerShell if you're on Windows).
- Example: ```ssh umdsecXX-xdc-umdsecXX``` where umdsecXX is the name of the user and the name of the project, with xdc being the name of the XDC.
2. To access your XDC <ins>with</ins> port-forwarding, you can type ```ssh -L port:node:80 username-xdc-proj```
- Example: ```ssh -L 8080:pathname:80 umdsecXX-xdc-umdsecXX``` where umdsecXX is the name of the user and the name of the project, with xdc being the name of the node. 8080 is an arbitrary number and can be a random four-digit number. node is the name of the materialization's node that you want to connect to. <ins>Read your lab manual if you're unsure what the name of your node is.<ins>
3. You will be asked to add two footprints when SSH'ing your first time. Type ```yes``` when prompted. The first one is to add Merge as a recognized host. The second one is to add your XDC as a recognized host. This only needs to be done once.

### Additional Notes:
- You are unable to do port-forwarding with more than one account. If you need to change accounts, please delete the ```Host mergejump``` and ```Host username-xdc-proj``` block from your ```config``` file and delete your ```merge-key``` file, both of which are located in ```~/.ssh/```. Then, re-run ```bash /share/port-forward-setup.sh``` on the Merge account which you want to port-forward from.
- If you are receiving an error which looks like ```Permission denied (publickey,keyboard-interactive)```, there is a possible bug from Merge. To fix this, navigate to ~/.ssh on your XDC and see if there's an ```authorized_keys``` file missing. If there is, create a new one with ```touch authorized_keys; sudo chmod 644 authorized_keys```, then run ```sudo cat merge_key.pub >> authorized_keys``` and try to SSH again.
