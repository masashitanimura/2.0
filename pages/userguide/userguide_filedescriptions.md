---
title: File Descriptions
sidebar: userguide_sidebar
permalink: userguide_filedescriptions.html
folder: userguide
toc: true
---

## Command Files

| File Name             | Description                              |
| --------------------- | ---------------------------------------- |
| emsTranscoder.bat     | The transcoder binary of EMS.            |
| evo-avconv(.exe)      | The EvoStream Transcoder binary. This gets called in reaction to the `transcode` API command. |
| evo-mp4writer(.exe)   | This binary application combines the various pieces of each MP4 recording once the file is ready to be finalized. |
| evo-node(.exe)        | The EvoStream Web Server (EWS) binary. This handles the serving of all files over HTTP. |
| evostreamms(.exe)     | The EvoStream binary itself.             |
| run_console_ems.bat   | Batch file/script which runs the EMS as a console application. This is useful for new users as it provides instant feedback on the console when commands are entered and shows errors if they occur in new streams. |
| run_console_webui.bat | Batch file/script which runs the EMS Web UI application. If you want a separate console for UI, you might want to run this binary. This is useful for new users as it provides instant feedback on the console when commands are entered and shows errors if they occur in new streams. |
| run_stop_webui.bat    | Batch file/script which **stops** the EMS Web UI application. |
| run_daemon_ems.sh     | Shell script used on **Linux/Unix** environments to start the EMS as a background application. Use this for production deployments. It requires that the user “evostream” exists, the script will not work without it. Please feel free to modify this script to use a different user. When using the daemon script, to validate that the server is running, you can issue the command `ps –ef` |
| run_console_ems.bat   | Batch file/script on **Windows** which runs the EMS as a console application. This is useful for new users as it provides instant feedback on the console when commands are entered and shows errors if they occur in new streams. |



## Windows Service Files

| File Name     | Description                              |
| ------------- | ---------------------------------------- |
| create.bat    | Script to create a Windows service for the EMS. This will also start the EMS as a background process. This must be run with Administrative privileges as it writes to the Windows Registry. *This only needs to be run once.* |
| remove.bat    | Script to remove the Windows service for the EMS and remove the relevant Windows Registry entries. This must be run with Administrative privileges. |
| start.bat     | Script to start the EMS Windows service. This script will not work if create.bat has not been run first. |
| stop.bat      | Script to stop the EMS Windows Service.  |
| uninstall.bat | Script used to uninstall EMS Windows Service during uninstallation. |



##Evo-Node Applications

| Application Name | Description                              |
| ---------------- | ---------------------------------------- |
| node-ews         | Contains the files for file serving and EMS-specific calls to group name aliasing apis, authproxy, etc. |
| node-webservices | Contains the files for the web services such as Upload HLS files to Amazon S3, Stream Load Balancer etc. |
| node-webui       | Contains the files for the EMS Web UI    |



## Configuration Files

| File Name           | Description                              |
| ------------------- | ---------------------------------------- |
| auth.xml            | The configuration of users.lua.          |
| bandwidthlimits.xml | Defines the maximum amount of bandwidth you want the server to be able to use (set the instantaneous bandwidth cap). |
| config.lua          | The main configuration file used by the EMS. The contents of this file are detailed later in this document. |
| connlimits.xml      | Defines the maximum number of concurrent connections you want the EMS to accept |
| ingestpoints.xml    | The configuration file where the ingest points are saved. |
| pushPullSetup.xml   | This file is used by the EMS to store stream action commands that are made through the Runtime API. This file may not be modified. At startup, if the EMS detects that the file has been modified it will rename the file and start with a blank/fresh copy. |
| users.lua           | Defines the valid authentication the server will require when streams are pushed into the EMS. |
| webconfig.json      | The EvoStream Web Server (EWS) configuration file. The contents of this file are detailed later in this document. |



## Documentation

| File Name                          | Description                              |
| ---------------------------------- | ---------------------------------------- |
| EvoStream Media Server EULA v2.pdf | The End User License Agreement for the EMS |



## Miscellaneous

| File/Folder Name       | Description                              |
| ---------------------- | ---------------------------------------- |
| blacklist.txt          | The list of the blacklisted IP addresses |
| whitelist.txt          | The list of the whitelisted IP addresses |
| server.key             | The private key used for security authentication. |
| server.cert            | The certificate used for security authentication. |
| tests.exe              | A binary file in Windows that performs series of tests to verify if there is an issue with your Windows. |
| platformTests          | A binary file in Linux that performs series of tests to verify if there is an issue with your Linux environment. |
| media/                 | The media directory is the default location for video-on-demand files. This is where the EMS will look when VOD requests are made. This default location can be changed in the EMS main configuration file, which is typically `config/config.lua` |
| logs/                  | This is the directory that EMS and EvoWebserver will write its logs to. This default location can be changed in the config.lua for EMS logs and webconfig.json for EvoWebserver logs. |
| License.lic            | This is the license file required to run the EMS. It can be placed in the `config/` , `bin/` , or `/etc/evostreamms/` folders, or in whatever folder the evostreamms binary resides. |
| /node-webservices/logs | The directory of the node-webservices logs. |
| /node-webui/logs       | The directory of the node-webui logs.    |

