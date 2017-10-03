---
title: Connecting to Web UI
sidebar: userguide_sidebar
permalink: userguide_connectui.html
folder: userguide
toc: true
---

## Automatic Start-up

If you started EMS and `rubWebUI` is `true` in config.lua, the EMS Web UI will also get started. All you need to do is to open the UI in your browser:

```
format: <EMS_IP>:<WebUI_Port>

sample: localhost:4100
```



## Manual Start-up

If you set `runWebUI` to `false` in config.lua, you can still run the UI via:



### Via Console

Starting the Web UI using `run_console_webui` will open a separate console for the Web UI. This is very helpful if you want to see solely logs from the Web UI. 

1. Run `run_console_webui.sh` in Linux,  `run_console_webui.bat` in Windows

   ![](images/userguide/startui_console.jpg)

   ​

2. Open the UI in your browser: 

   ```
   format: <EMS_IP>:<WebUI_Port>

   sample: localhost:4100
   ```


​      **Note:**

   - You may configure the logging level of UI in `../node-webui/config/logging.json`




### Via Daemon

For Linux environment only, running Web UI via Daemon mode is also available. This will not show a console showing the logs of the activities of the Web UI.  

1. Run `run_daemon_webui.sh`

2. Open the UI in your browser: 

   ```
   format: <EMS_IP>:<WebUI_Port>

   sample: localhost:4100
   ```

   **Notes:**

   - Run `ps -ef|grep node` to see if Web UI is running, you should see `./evo-node node-webui/bin/webui_activate` in the result
   - You may check the Web UI logs in `../node-webui/logs/`
   - The configuration of the log level is the same with console logs and file logs

   ​




## Stopping Web UI

If you run the UI using the `run_console_webui.bat` or `run_console_webui.sh` or `run_daemon_ems.sh`:

1. Run `run_stop_webui.bat` in Windows or `run_stop_webui.sh` in Linux

   ```
   $ ./run_stop_webui.sh 
   webui will now be stopped
   ```

This will end the process of the Web UI running.
