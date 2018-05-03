# WebMeet
A web component that can be embedded in a web site to enable live meetings with Openfire users

## Introduction
This is a full-featured web chat component that can be added to any web page. 
The component allows visitors to a web site to chat directly with members of a work group or team in a multi-user chat (MUC) through an integrated web client. The web component can be customised and re-branded with HTML/CSS.

It embeds [http://www.conversejs.org](converse.js) in the web site to handle the messaging with Openfire and depeding on configuration, it can open a windows for a video-conference using [http://github.com/igniterealtime/Openfire-Meetings](Openfire Meetings) or a telephone conference call using [http://freeswitch.org/confluence/display/FREESWITCH/Verto+Communicator](FreeSWITCH Verto Communicator).


This is how to add webmeet to your web site in a few simple steps.

## How to do it

Let’s assume that you have the following pre-existing index.html page on your web site:

`````
<html>
  <body>
    <h1>This is my web site!</h1>
    <p>Welcome!</p>
  </body>
</html>
`````
Now, you want to add the WebMeet component. You can do that before the </body> tag with lines of code:

`````
<html>
  <body>
    <h1>This is my web site!</h1>
    <p>Welcome!</p>

    <link type="text/css" rel="stylesheet" href="ofmeet.css">
    <script src="ofmeet.js"></script>
    
  </body>
</html>
`````
The <script/> tag above brings in the WebMeet web control and the <link/> tag brings in the default css file to style it. 
Copy the verto and ofmeet folders to the same folder as your index.html page. Thats it!!

## Additional considerations

The defult configuration for converse.js is to assume that Openfire and FreeSWITCH are on the same host as the web server and uses window.hostname as the XMPP and SIP domain names. Edit ofmeet/convese.html to match your preference.

`````
    converse.initialize({
        authentication: 'anonymous',
        auto_login: true,
        auto_join_rooms: [
            'lobby@conference.' + location.hostname,
        ],
        play_sounds: true,
        sounds_path: "sounds/",
        notification_icon: "image.png",
        muc_domain: "conference." + location.hostname,
        domain_placeholder: location.hostname,
        registration_domain: location.hostname,
        locked_domain: location.hostname,
        whitelisted_plugins: ["converse-singleton", "converse-inverse", "ofmeet"],
        blacklisted_plugins: ["converse-minimize", "converse-dragresize"],
        bosh_service_url: 'https://' + location.host + '/http-bind/',
        websocket_url: 'wss://' + location.host + '/ws/',
        jid: location.hostname,
        notify_all_room_messages: true,
        auto_reconnect: true,
        allow_non_roster_messaging: true,
        view_mode: 'embedded',
        ofmeet_invitation: 'Please join meeting at:',
        ofswitch: false
    });
`````
