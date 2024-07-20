# ExtraWSL

##
Useful tools & Custom image installer (you can almost install any linux distro)



<b>Amazon Linux 2023 on WSL2<b/>
![image](https://github.com/user-attachments/assets/980bcb0f-aab3-4197-8a30-552759d4de76)



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
