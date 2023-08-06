# UPDATE THE SYSTEM AND INSTALLATION OF SKYPE, GOOGLE-CHROME, ANYDESK AND VS-CODE

# Automated Installation Script

This script automates the installation of packages using both `apt` and `snap` package managers. It manages package updates, downloads and installs specific packages, and handles dependencies.

## Usage

1. Open a terminal and switch to the root user:

    ```bash
    sudo -i
    ```

2. Create a new file named `script.sh` and open it with the `vim` text editor:

    ```bash
    vim script.sh
    ```

3. Copy and paste the following script content into the `script.sh` file:


```
    
#!/bin/bash

# Colors for formatting output
Green='\033[0;92m'
Red='\033[0;91m'
Yellow='\033[0;33m'
NC='\033[0m' # No Color

apt_manage() {
    echo "${Yellow}Managing packages with apt...${NC}"
    apt update
    apt --fix-broken install -y
    apt upgrade -y
    echo "${Green} Done.${NC}"
}


install_with_snap() {
    package_name=$1
    if ! which "$package_name" > /dev/null 2>&1; then
        echo "${Yellow}Package $package_name is not available. ${Green}Installing...${NC}"
        sleep 2
        snap install $package_name --classic > /dev/null 2>&1
        if [ $? -eq 0 ]; then
            echo "${Green} Package $package_name is successfully installed.${NC}"
        else
            echo "${Red} Package $package_name installation failed.${NC}"
        fi
    else
        echo "${Green} Package $package_name is already available. No need to install.${NC}"
    fi
    echo ""
    sleep 2
}


install_dir="/home/intersoft-admin/installation-of-package"

# Create the installation directory if it doesn't exist
if [ ! -d "$install_dir" ]; then
    mkdir -p "$install_dir"
fi

apt_manage

# Refresh snap
echo "${Yellow}Updating snap...${NC}"
snap refresh
echo "${Green} Done.${NC}"

# Download AnyDesk package
echo "${Yellow}Downloading AnyDesk package...${NC}"
wget https://download.anydesk.com/linux/anydesk_6.2.1-1_amd64.deb -O $install_dir/anydesk_6.2.1-1_amd64.deb > /dev/null
echo "${Green} Done.${NC}"

# Download Google Chrome package
echo "${Yellow}Downloading Google Chrome package...${NC}"
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb -O $install_dir/google-chrome-stable_current_amd64.deb > /dev/null
echo "${Green} Done.${NC}"

# Install downloaded packages using dpkg -i
echo "${Yellow}Installing downloaded packages...${NC}"
dpkg -i $install_dir/*.deb > /dev/null 2>&1
echo "${Green} Done.${NC}"

install_with_snap "code"
install_with_snap "skype"

# Fix broken dependencies again
apt_manage

# Clean up
echo "${Green}Cleaning up...${NC}"
rm -f "$install_dir"/* > /dev/null 2>&1
rmdir "$install_dir" > /dev/null 2>&1
echo "${Green} Done.${NC}"

```

> Save the file and exit the `vim` editor. Press `Esc`, then type `:wq` and press `Enter`.

4. Run the following command to execute the script:

    ```bash
    sh script.sh
    ```

5. After running the command, you will see the output as shown in the image. At this point, please press the **Enter** key.
    <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/installation_of_some_packages-AIT/blob/802bbdc619aa283ab155ef289aba7fee280db0db/Picture-data/1.png">

6. After pressing **Enter** once, you will receive another set of distinct outputs, as indicated in the image. Once again, proceed by pressing the **Enter** key. Avoid any other actions at this stage.
    <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/installation_of_some_packages-AIT/blob/802bbdc619aa283ab155ef289aba7fee280db0db/Picture-data/2.png">


> **NOTE:** Now, simply relax and wait. The script will take care of the entire installation process automatically. No further actions are required from your end.

<div align="center">
  
# END

</div>
