---
title: Installation on Linux OS
sidebar: userguide_sidebar
permalink: userguide_installlinuxos.html
folder: userguide
toc: true
---



## Platform Verification

If you are unsure if the distribution you downloaded is appropriate for your Operating System, you can use the `platformTests` program. This program is available with all distributions and provides a suite of platform compatibility tests. It can be found in the bin directory.

On all systems, open a console or terminal (command prompt) and run the `platformTests` executable (`./platformTests`). It will print out the results of the platform compatibility tests. If the test succeeds, then you have an appropriate distribution!



## Linux Limitations

Linux systems place limits on the number of sockets and file descriptors a process may use. This will apply to the EMS as well. If you plan on using more than 1024 connections at one time for your server, you will need to modify the following configuration file: `/etc/security/limits.conf`

The following lines will need to be added/modified:

```
soft nofile 16384
hard nofile 65536
soft nproc 4096
hard nproc 16384
```

## Installation Procedure

### Linux Package (Linux apt/yum Installer)

**Pre-requisites:**

Administrative privileges are required. This can be accomplished in many ways.

If the sudo utility is available:

```
$ su –
```

If the sudo utility is not available:

```
$ sudo su –
```

**Note:**

The prompt changes from `$` to `#` when administrative privileges are enabled.



**Installation Procedure:**

1\. Retrieve the script used to install the EvoStream software repository and store it

- Debian based Linux distributions (Ubuntu or Debian)

  ```
  # wget http://apt.evostream.com/installkeys.sh -O /tmp/installkeys.sh
  ```

- RedHat based Linux distributions (CentOS, Fedora, RHEL)

  ```
  # curl http://yum.evostream.com/installkeys.sh -o /tmp/installkeys.sh
  ```

  ​

2\. Execute the script to install the EvoStream software repository and keys

```
# sh /tmp/installkeys.sh
```

- If successful, the following message should be printed on the console:

  ```
  "EvoStream keys installed successfully"
  ```

At this stage, the EvoStream software repository and keys are successfully installed and you can install packages from it.

**Note:** Steps 1 and 2 above must be executed only once.

The following steps are used to install the EvoStream Media Server, and can be repeated to update the EMS to the most recent release.



3\. Install EvoStream Media Server.

- Debian based Linux distributions (Ubuntu or Debian)

  ```
  # apt-get install evostream-mediaserver
  ```

- RedHat based Linux distributions (CentOS, Fedora, RHEL)

  ```
  # yum install evostream-mediaserver
  ```




#### License Installation

To install the license, simply copy the `License.lic` file to `/etc/evostream/License.lic`.



### Linux Archive (.tar.gz Distribution)

You can install the EMS from a simple archive file (.tar.gz). The latest EMS Release can be found on the EvoStream website: [https://evostream.com/software-downloads/](https://evostream.com/software-downloads/).

You will need to choose the most appropriate distribution for the Operating System that you are using. Once you have downloaded your distribution.

Simply **extract** the EMS package. The location of the installation is not important. However, for security reasons, the EvoStream Media Server should **NOT** be installed into the web-root of the target computer (if one exists).



#### License Installation

To install the license, simply copy the `License.lic` file to `../config/License.lic`.





## Distribution Content

### Linux Package

**A.1. Configuration files**

```
├── etc
│   └── evostreamms
│       ├── blacklist.txt
│       ├── config.lua
│       ├── server.cert
│       ├── server.key
│       ├── users.lua
│       ├── webconfig.lua
│       └── whitelist.txt
```

**A. 2. XXX Files**

```
├── usr
│   ├── bin
│   │   ├── evo-phpengine
│   │   │   └── php.cgi
│   │   ├── evo-avconv
│   │   ├── evo-mp4writer
│   │   ├── evostreamms
│   │   └── evo-webserver
│   └── share
│       ├── evo-avconv
│       │   └── presets
│       │       └── [30 transcode preset files]
│       └── doc
│           └── evostreamms
│               ├── copyright
│               ├── EvoStream Media Server EULA v2.pdf
│               ├── README.txt
│               └── version
│                   ├── BUILD_DATE
│                   ├── BUILD_NUMBER
│                   ├── CODE_NAME
│                   ├── OS_NAME
│                   ├── OS_VERSION
│                   └── RELEASE_NUMBER
```

**A.3. XML Files**

```
└── var
    ├── evostreamms
    │   ├── media
    │   └── xml
    │       ├── auth.xml
    │       ├── bandwidthlimits.xml
    │       ├── connlimits.xml
    │       ├── ingestpoints.xml
    │       └── pushPullSetup.xml
```

**A.4. HTML and evowebservices Files**

```
└── var
    ├── evo-webroot
    │   ├── demo
    │   │   ├── css
    │   │   ├── evo.png
    │   │   ├── evowrtcclient.html
    │   │   ├── evowsvideo.html
    │   │   ├── jsonMetaTest.html
    │   │   ├── jsonMetaWriteTest.html
    │   │   └── loading.gif
    │   ├── evowebservices
    │   │   ├── config
    │   │   ├── core
    │   │   ├── plugins
    │   │   ├── evostream_copyright.txt
    │   │   ├── evowebservices.php
    │   │   └── README.txt
    │   ├── clientaccesspolicy.xml
    │   └── crossdomaim.xml
```

**A.5. Log Files**

```
└── var
    ├── log
    │   └── evostreamms
```

**A.6. Executable Files**

```
└── var
    └── run
        └── evostreamms
```





### Linux Archive

```
./EvoStream Archive
  ├── bin
  │   ├── evo-phpengine
  │   ├── emsTranscoder.sh
  │   ├── evo-avconv
  │   ├── evo-mp4writer
  │   ├── evostreamms
  │   ├── evo-webserver
  │   ├── platformTests
  │   ├── run_console_ems.sh
  │   └── run_daemon_ems.sh
  ├── config
  │   ├── auth.xml
  │   ├── bandwidthlimits.xml
  │   ├── blacklist.txt
  │   ├── config.lua
  │   ├── connlimits.xml
  │   ├── ingestpoints.cml
  │   ├── pushPullSetup.xml
  │   ├── server.cert
  │   ├── server.key
  │   ├── users.lua
  │   ├── webconfig.lua
  │   └── whitelist.txt
  ├── demo
  │   ├── base64.js
  │   └── emsdemo.html
  ├── evo-avconv-presets
  │   └── [30 transcode preset files]
  ├── evo-webroot
      ├── demo
      │   ├── css
      │   ├── evo.png
      │   ├── evowrtcclient.html
      │   ├── evowsvideo.html
      │   ├── jsonMetaTest.html
      │   ├── jsonMetaWriteTest.html
      │   └── loading.gif
      ├── evowebservices
      │   ├── config
      │   ├── core
      │   ├── plugins
      │   ├── EMS_Web_Services_User_Guide.pdf
      │   ├── evostream_copyright.txt
      │   └── evowebservices.php
      ├── clientaccesspolicy.xml
      └── crossdomain.xml
  ├── logs
  ├── media
  ├── BUILD_DATE
  ├── Evostream Media Server EULA v2.pdf
  └── README.txt
```



