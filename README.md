# Table of Contents

1. [Introduction](#introduction)
2. [Example 1 -> Export Docker Container's Rootfs and Import to WSL](#example-1--export-docker-containers-rootfs-and-import-to-wsl)
3. [Overview](#overview)
4. [Components](#components)
   - [WslInstall](#wslinstall)
   - [ConfigDistro](#configdistro)
   - [GetDistroConfig](#getdistroconfig)
   - [IsDistroRegistered](#isdistroregistered)
   - [LaunchDistro](#launchdistro)
   - [LaunchIntDistro](#launchintdistro)
   - [RegisterDistro](#registerdistro)
   - [UnregisterDistro](#unregisterdistro)
5. [Structure](#structure)
6. [Building the Project](#building-the-project)


# ExtraWSL

##
Useful tools & Custom image installer (you can almost install any linux distro)



<b>Amazon Linux 2023 on WSL2<b/>
![image](https://github.com/user-attachments/assets/980bcb0f-aab3-4197-8a30-552759d4de76)



## Example 1 -> export Docker container's rootfs then import to WSL

You can easily obtain the root filesystem (rootfs) of any distribution using docker container.

Example:

Select any distribution from Docker Hub.

After pulling it, export the tarball to the host machine.

To export it, run the following command: 
* `docker export <container_id_or_name> -o host_path` 

For example:

* `docker export ea153aa76c2867a8b7f959f92b4d68238ae6ece3f38178a2bc304dcc90ee2035 -o rootfs.tar`


![image](https://github.com/user-attachments/assets/c18dedf8-22fa-49c4-a440-2b387fe6bc6e)

If you haven't already cloned this repository, do so now:
<br>
* `git clone https://github.com/csabika98/ExtraWSL`  
To import and register the Docker container, follow these steps:

![image](https://github.com/user-attachments/assets/7f82d1f6-268f-4762-bfef-6fd3df968165)

Navigate to the "Release" directory, then run WslInstall.exe with the following syntax:
<br>
* `syntax: .exe <distro_name> <rootfs_path>`

![image](https://github.com/user-attachments/assets/8dd8da07-99bb-432f-8f41-bce0134ba37c)

WslInstall will convert `tar` to `vhdx`, and it will register the distro

You are almost done! To verify run: 
* `run wsl -l` 

You should see your new distribution listed.
<br>
![image](https://github.com/user-attachments/assets/5239293d-09cd-4c79-9749-2a9274f2941d)

To run the new distro, type the following:
* `wsl -d <distro_name_you_added_>` and voilá. Enjoy

## Overview
WSLExtra is a suite of utilities designed to simplify the management and interaction with Windows Subsystem for Linux (WSL) distributions. 

This collection of tools enables users to configure, retrieve information, register, and unregister WSL distributions, as well as install new GNU/Linux distributions.

## Components

# 1. WslInstall
**Description:**  
Installs GNU/Linux distributions from tarball archives.

**Usage:**  
1. Create a folder where you want to install the distribution.
2. Place `WslInstall.exe` and `{distribution}.tar.gz` in the same folder.
3. Open Command Prompt in that folder and run:

    `WslInstall.exe <distro_name> <distribution.tar.gz>`

- **distro_name:** The name of the distribution.
- **distribution.tar.gz:** The tarball file containing the distribution.

**Example:**  
`WslInstall.exe Ubuntu ubuntu.tar.gz`

This command installs the Ubuntu distribution from `ubuntu.tar.gz`. After installation, confirm the distribution with:

`wslconfig.exe /list /all`

You should see a root filesystem folder in the directory where you installed the distribution.


# 2. ConfigDistro
**Description:**  
Configures a WSL distribution by setting the default user ID and distribution flags.

**Usage:**  
`ConfigDistro.exe <distro_name> <default_user_id> <distribution_flags>`

- **distro_name:** The name of the WSL distribution.
- **default_user_id:** The default user ID to set.
- **distribution_flags:** Flags to configure the distribution.

**Example:**  
`ConfigDistro.exe Ubuntu 1000 WSL_DISTRIBUTION_FLAGS_DEFAULT`

This command configures the Ubuntu distribution with a default user ID of 1000 and the default distribution flags.

# 3. GetDistroConfig
**Description:**  
Fetches and displays configuration details of a WSL distribution including version, default user ID, flags, and environment variables.

**Usage:**  
`GetDistroConfig.exe <distro_name>`

- **distro_name:** The name of the WSL distribution.

**Example:**  
`GetDistroConfig.exe Ubuntu`

**Output Example:**

Version: 2
DefaultUID: 1000
WslFlags: 15
Default Environment Variables Array: HOSTTYPE=x86_64
Default Environment Variables Count: 4


# 4. IsDistroRegistered
**Description:**  
Checks if a WSL distribution is registered and available for use.

**Usage:**  
`IsDistroRegistered.exe <distro_name>`

- **distro_name:** The name of the WSL distribution.

# 5. LaunchDistro
**Description:**  
Launches the specified Linux distribution.

**Usage:**  
`LaunchDistro.exe <distro_name>`

- **distro_name:** The name of the WSL distribution.

# 6. LaunchIntDistro
**Description:**  
Launches an internal Linux distribution, typically used for testing or specific scenarios.

**Usage:**  
`LaunchIntDistro.exe <distro_name>`

- **distro_name:** The name of the WSL distribution.

# 7. RegisterDistro
**Description:**  
Registers a new WSL distribution.

**Usage:**  
`RegisterDistro.exe <distro_name>`

- **distro_name:** The name of the WSL distribution to register.

# 8. UnregisterDistro
**Description:**  
Unregisters an existing WSL distribution.

**Usage:**  
`UnregisterDistro.exe <distro_name>`

- **distro_name:** The name of the WSL distribution to unregister.


# Structure

├── ConfigDistro.c

├── ConfigDistro.vcxproj

├── DistroLink.cpp

├── DistroLink.vcxproj

├── GetDistroConfig.c

├── GetDistroConfig.vcxproj

├── IsDistroRegistered.c

├── IsDistroRegistered.vcxproj

├── LaunchDistro.c

├── LaunchDistro.vcxproj

├── LaunchIntDistro.c

├── LaunchIntDistro.vcxproj

├── Makefile

├── RegisterDistro.c

├── RegisterDistro.vcxproj

├── UnregisterDistro.c

├── UnregisterDistro.vcxproj

├── lib/

│ ├── wslapi.lib

│ ├── ole32.lib

│ └── shell32.lib

├── Release/


└── .gitignore


# Building the Project


1. Open Developer Command Prompt for Visual Studio.
2. Navigate to Your Project Directory:

    `cd C:\Users\DEV\Desktop\WSLInstall\WslFunctions2`

3. Build Each Project:

    For each `.vcxproj` file, run:

    `msbuild <project_name>.vcxproj /p:Configuration=Release /p:Platform=x64`

    Replace `<project_name>` with the appropriate project file name.

**Example:**  
`msbuild ConfigDistro.vcxproj /p:Configuration=Release /p:Platform=x64`
