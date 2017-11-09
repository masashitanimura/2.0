---
title: EMS Integration Ready Player Libraries
keywords: js
sidebar: html5players_sidebar
permalink: html5players_emsjslib.html
folder: html5players
toc: false
---

Below is the sample code (EMS JS libraries) that can be used for browsers, iOS and Android Players:

```
<html>
	<head>
		<script src="./js/evohtml5player-latest.bundle.js"></script>   <--(1) Import the Evostream JSPlayer Bundle
			:
			:
			:
	</head>
	<body>
			:
			:
		<video id="myVideo"></video> <--(2) Declare a video tag, and make sure to assign an element ID.
			:
			:
			
		<script>
			function playViaWebSocket() {  <--(3) Call this if you want to play a stream via WebSockets
				var options = {
					emsIp: "192.168.10.10", // set this to the IP address of your EMS instance
					streamName: "myStream", // set this to the stream that you wish to play
					videoTagId: "myVideo"   // set this to the element ID of your video tag.
				};
				var emsPlayer = new EvoWsPlayer ( options );
				emsPlayer.play();
			}
			
			function playViaWebRtc() {  <-- (4) Call this is you want to play a stream using WebRTC
				var options = {
                   	ersIp: "10.10.20.30",	// set this to the IP address of your ERS
				 port:  4545,			// set this to the PORT that your ERS is configured to
				 streamName: "myStream",  // set this to the stream that you wish to play
				 videoTagId: "myVideo"    // set this to the element ID of your video tag.
                    roomName:   "myRoom",	// set this to that room that EMS is configured to
                };

				var emsPlayer = new EvoWrtcPlayer ( options );
				emsPlayer.play();
			}
		</script>
	</body>
</html>	
```

