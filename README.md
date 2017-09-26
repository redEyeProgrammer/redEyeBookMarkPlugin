# redEyeBookMarkPlugin
How to use Plugin:
**Note -> See this sample Demo application (https://github.com/redEyeProgrammer/PluginSampleApplication.git) that uses myHybridPlugin and configure your testApp accordingly

 Create a test application from Terminal (testApp would consume this Plugin)

cordova create testapp com.redEye.testapp TestApp (use your bundleIdentifier of choice)
cd testapp

cordova plugin add cordova-plugin-add-swift-support --save (plugin that will install the bridging header for Swift files)

cordova platform add ios

cordova build ios

Open ProjectWorkspace and do the following. Create a storyboard name Main
Make Main Storyboard the Main interface in Project settings
Open Main Storyboard and Create TabBarController
Make first item of tabBarController inherit MainViewController (that came pre-added)
Make Second item inherit tableViewController (and make the VC in storyboard a TableViewController)


**Note -> See this sample Demo application (https://github.com/redEyeProgrammer/PluginSampleApplication.git) that uses myHybridPlugin and configure your testApp accordingly


Configure index.js:
/*
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing,
 * software distributed under the License is distributed on an
 * "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 * KIND, either express or implied.  See the License for the
 * specific language governing permissions and limitations
 * under the License.
 */
var app = {
    // Application Constructor
initialize: function () {
    this.bindEvents();
},
    // Bind Event Listeners
    //
    // Bind any events that are required on startup. Common events are:
    // 'load', 'deviceready', 'offline', and 'online'.
bindEvents: function () {
    document.addEventListener('deviceready', this.onDeviceReady, false);
    
},
    // deviceready Event Handler
    //
    // The scope of 'this' is the event. In order to call the 'receivedEvent'
    // function, we must explicitly call 'app.receivedEvent(...);'
onDeviceReady: function() {
    //app.receivedEvent('deviceready');
    document.getElementById("bookmarkBtn").onclick = app.addBookmark;
    document.getElementById("requestBtn").onclick = app.makeRequest;
},
    
    // Update DOM on a Received Event
receivedEvent: function(id) {
    var parentElement = document.getElementById(id);
    var listeningElement = parentElement.querySelector('.listening');
    var receivedElement = parentElement.querySelector('.received');
    
    listeningElement.setAttribute('style', 'display:none;');
    receivedElement.setAttribute('style', 'display:block;');
    
    console.log('Received Event: ' + id);
},
    
makeRequest: function() {
    var xhttp = new XMLHttpRequest();
    xhttp.open("POST", "http://jsonplaceholder.typicode.com/users/1", false);
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send();
    var response = JSON.parse(xhttp.responseText);
    alert(response)
},
    
addBookmark: function() {
    console.log("Called add bookmark");
    var win = function(d) {
        console.log("Bookmark added!");
    };
    var fail = function(e) {
        console.log(e)
    }
    var bookmark = document.getElementById("bookmark").value
    if (!document.getElementById("bookmark").value) {
        alert("Text Empty");
    } else {
        cordova.exec(win, fail, "MyHybridPlugin", "addBookmark", [bookmark]);
        alert("BookMark Added");
        document.getElementById("bookmark").value = "";
        
    }
}
    
    
};

app.initialize();




Configure index.html:
<!DOCTYPE html>
<!--
 Licensed to the Apache Software Foundation (ASF) under one
 or more contributor license agreements.  See the NOTICE file
 distributed with this work for additional information
 regarding copyright ownership.  The ASF licenses this file
 to you under the Apache License, Version 2.0 (the
 "License"); you may not use this file except in compliance
 with the License.  You may obtain a copy of the License at
 
 http://www.apache.org/licenses/LICENSE-2.0
 
 Unless required by applicable law or agreed to in writing,
 software distributed under the License is distributed on an
 "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 KIND, either express or implied.  See the License for the
 specific language governing permissions and limitations
 under the License.
 -->
<html>
    <head>
        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap:; style-src 'self' 'unsafe-inline'; media-src *">
            <meta name="format-detection" content="telephone=no">
                <meta name="msapplication-tap-highlight" content="no">
                    <meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width">
                        <link rel="stylesheet" type="text/css" href="css/index.css">
                            <title>Hello World</title>
                            </head>
    <body>
     
        <div class="app">
            <label for="bookmark">Bookmark this:</label>
            <input id="bookmark" type="text" />
            <button id="bookmarkBtn" onclick="app.addBookmark()">Add a bookmark</button>
        </div>
        <script type="text/javascript" src="cordova.js"></script>
        <script type="text/javascript" src="js/index.js"></script>
    </body>
</html>

