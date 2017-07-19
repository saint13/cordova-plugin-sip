# cordova-plugin-sip
<h2>SIP plugin for Cordova Apps (IOS and Android)</h2>

<h3>IOS</h3>

<h4>Build Settings -> Header Search Paths</h4>
<code>

    "$(SRCROOT)/YOURPROJECTNAME/Plugins/cordova-plugin-sip/include"
    "$(SRCROOT)/YOURPROJECTNAME/Plugins/cordova-plugin-sip/include/belle-sip"
    "$(SRCROOT)/YOURPROJECTNAME/Plugins/cordova-plugin-sip/include/ortp"
    "$(SRCROOT)/YOURPROJECTNAME/Plugins/cordova-plugin-sip/include/linphone"
    "$(SRCROOT)/YOURPROJECTNAME/Plugins/cordova-plugin-sip/include/mediastreamer2"
</code>

<h4>You must import these files in the  Bridging Header File</h4>
<code>

    #include "Plugins/cordova-plugin-sip/include/linphone/lpconfig.h"
    #include "Plugins/cordova-plugin-sip/include/linphone/linphonecore.h"
    #include "Plugins/cordova-plugin-sip/include/linphone/linphonecore_utils.h"
</code>

<h4>IOS Permissions</h4>
  
You must include following permissions
<code>

        <key>NSCameraUsageDescription</key>
        <string>Description Why you use this permission</string>
        <key>NSMicrophoneUsageDescription</key>
        <string>Description Why you use this permission</string>
</code>


<h3>Android </h3>

Deploy and Run!



<h3>Usage</h3>
<code>


    var sipManager = {
        register: function () {
            cordova.plugins.sip.login('203', '203', '192.168.1.111:5060', function (e) {

                if (e == 'RegistrationSuccess') {
                    console.log(e);
                    sipManager.listen();
                } else {
                    alert("Registration Failed!");
                }

            }, function (e) { console.log(e) })
        },
        call: function () {
            cordova.plugins.sip.call('sip:111@192.168.1.111:5060', '203', sipManager.events, sipManager.events)
        },
        listen: function () {
            cordova.plugins.sip.listenCall(sipManager.events, sipManager.events);
        },
        hangup: function () {
            cordova.plugins.sip.hangup(function (e) { console.log(e) }, function (e) { console.log(e) })
        },
        events: function (e) {
            console.log(e);
            if (e == 'Incoming') {
                var r = confirm("Incoming Call");
                if (r == true) {
                    cordova.plugins.sip.accept(true, sipManager.events, sipManager.events);
                } else {

                }
            }
            if (e == 'Connected') {
                alert("Connected!");
                sipManager.listen();
            }
            if (e == 'Error') {
                alert("Call Error!");
                sipManager.listen();
            }
            if (e == 'End') {
                alert("Call End!");
                sipManager.listen();
            }


        }
    }
</code>
