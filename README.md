# Completed Labs

## Lab 1 Internet of Things
Make sure the following services are provisioned
- IoT Foundation
- DashDB

### Make sure you have created your **NodeRed** application

1. Start your NodeRed application and click **Connections** link on the left navigation.
2. You should see a tile for the "Cloudant" service. If you do not see a tile for "dashDB" or the "IoT Foundation", you must add them by clicking on the **connect existing** button on the right.
3. You should be prompted with a list of tiles for "Conversation", "dashDB", and "Internet of Things". Select one tile at a time and then click the **Connect** button. You will be prompted to restage, click **restage**.
4. Once all of the services are connected to the application, you can click on the **visit App URL** link at the top of the page. This will take you to the NodeRed Editor.

### Add IoT Flow to Editor

Copy the text below

```JSON
[
    {
        "id": "3ab980c7.4610c",
        "type": "tab",
        "label": "Bluemix IoT Flows"
    },
    {
        "id": "e2cf6c74.fdc4d",
        "type": "ibmiot in",
        "z": "3ab980c7.4610c",
        "authentication": "apiKey",
        "apiKey": "8a8775f1.72ea58",
        "inputType": "evt",
        "deviceId": "JeffPiGateway",
        "applicationId": "",
        "deviceType": "PiGateway",
        "eventType": "environment",
        "commandType": "",
        "format": "json",
        "name": "IoT : environment",
        "service": "registered",
        "allDevices": true,
        "allApplications": "",
        "allDeviceTypes": true,
        "allEvents": false,
        "allCommands": "",
        "allFormats": false,
        "qos": 0,
        "x": 186.25000953674316,
        "y": 288.75000190734863,
        "wires": [
            [
                "ae593a8d.0ade98",
                "50cd13b4.b3769c",
                "f8160c87.24af3"
            ]
        ]
    },
    {
        "id": "50cd13b4.b3769c",
        "type": "debug",
        "z": "3ab980c7.4610c",
        "name": "debug : sensor data",
        "active": false,
        "console": "false",
        "complete": "true",
        "x": 466.25000953674316,
        "y": 348.75000190734863,
        "wires": []
    },
    {
        "id": "ae593a8d.0ade98",
        "type": "function",
        "z": "3ab980c7.4610c",
        "name": "format : environment data for DB",
        "func": "// Format Sensor Data for dashDB\nmsg.payload = {\n    SENSORID : msg.deviceId,\n    TEMPERATURE : msg.payload.d.temperature,\n    HUMIDITY : msg.payload.d.humidity,\n    PRESSURE : msg.payload.d.pressure,\n    TIMESENT : 'TIMESTAMP'\n};\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 506.25000953674316,
        "y": 288.75000190734863,
        "wires": [
            [
                "c9f4ca.89f5ab38",
                "88d97594.45b808"
            ]
        ]
    },
    {
        "id": "c9f4ca.89f5ab38",
        "type": "debug",
        "z": "3ab980c7.4610c",
        "name": "debug : dashDB data",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 806.2500095367432,
        "y": 348.75000190734863,
        "wires": []
    },
    {
        "id": "88d97594.45b808",
        "type": "dashDB out",
        "z": "3ab980c7.4610c",
        "dashDB": "9daa45bb.2be6c8",
        "service": "_ext_",
        "table": "SENSEDATA",
        "name": "dashDB",
        "x": 766.2500095367432,
        "y": 288.75000190734863,
        "wires": []
    },
    {
        "id": "c2642381.924ad",
        "type": "comment",
        "z": "3ab980c7.4610c",
        "name": "Receive IoT events from Sense Hat",
        "info": "",
        "x": 246.25000953674316,
        "y": 248.75000190734863,
        "wires": []
    },
    {
        "id": "70dd05e4.0407ec",
        "type": "ibmiot in",
        "z": "3ab980c7.4610c",
        "authentication": "boundService",
        "apiKey": "",
        "inputType": "evt",
        "deviceId": "",
        "applicationId": "",
        "deviceType": "",
        "eventType": "motion",
        "commandType": "",
        "format": "json",
        "name": "IoT : motion",
        "service": "registered",
        "allDevices": true,
        "allApplications": "",
        "allDeviceTypes": true,
        "allEvents": false,
        "allCommands": "",
        "allFormats": "",
        "qos": 0,
        "x": 176.25000953674316,
        "y": 348.75000190734863,
        "wires": [
            [
                "50cd13b4.b3769c"
            ]
        ]
    },
    {
        "id": "e2afe297.1baff",
        "type": "ibmiot in",
        "z": "3ab980c7.4610c",
        "authentication": "boundService",
        "apiKey": "",
        "inputType": "evt",
        "deviceId": "",
        "applicationId": "",
        "deviceType": "+",
        "eventType": "joystick",
        "commandType": "",
        "format": "json",
        "name": "IoT : joystick",
        "service": "registered",
        "allDevices": true,
        "allApplications": "",
        "allDeviceTypes": true,
        "allEvents": "",
        "allCommands": "",
        "allFormats": "",
        "qos": 0,
        "x": 176.25000953674316,
        "y": 408.75000190734863,
        "wires": [
            [
                "50cd13b4.b3769c"
            ]
        ]
    },
    {
        "id": "8c35c049.f5b38",
        "type": "ibmiot out",
        "z": "3ab980c7.4610c",
        "authentication": "apiKey",
        "apiKey": "8a8775f1.72ea58",
        "outputType": "cmd",
        "deviceId": "JeffSenseHat-001",
        "deviceType": "PiGateway",
        "eventCommandType": "message",
        "format": "json",
        "data": "data",
        "qos": 0,
        "name": "IoT : commands",
        "service": "registered",
        "x": 835.2500095367432,
        "y": 570.7500019073486,
        "wires": []
    },
    {
        "id": "b2ab47f0.8148a8",
        "type": "inject",
        "z": "3ab980c7.4610c",
        "name": "test : alarm",
        "topic": "alarm",
        "payload": "navy",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "x": 186.25000953674316,
        "y": 588.7500019073486,
        "wires": [
            [
                "26579600.dc41da"
            ]
        ]
    },
    {
        "id": "26579600.dc41da",
        "type": "function",
        "z": "3ab980c7.4610c",
        "name": "format : command test",
        "func": "if (msg.topic == \"alarm\") {\n  msg.eventOrCommandType = \"alarm\";\n  msg.payload={d:{color:msg.payload}};\n}\nelse if (msg.topic == \"message\") {\n  msg.eventOrCommandType = \"message\";\n  msg.payload={d:{color:\"blue\",\n                  background:\"red\",\n                  message:msg.payload}};\n}\nelse\n  msg = null;\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 466.25000953674316,
        "y": 528.7500019073486,
        "wires": [
            [
                "8c35c049.f5b38",
                "6e80296f.d605b8"
            ]
        ]
    },
    {
        "id": "cd4cf4c2.1e57c8",
        "type": "inject",
        "z": "3ab980c7.4610c",
        "name": "test : LED off",
        "topic": "alarm",
        "payload": "off",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "x": 196.25000953674316,
        "y": 528.7500019073486,
        "wires": [
            [
                "26579600.dc41da"
            ]
        ]
    },
    {
        "id": "6e80296f.d605b8",
        "type": "debug",
        "z": "3ab980c7.4610c",
        "name": "debug : IoT commands",
        "active": false,
        "console": "false",
        "complete": "true",
        "x": 803.2500095367432,
        "y": 640.7500019073486,
        "wires": []
    },
    {
        "id": "c817a232.531aa",
        "type": "inject",
        "z": "3ab980c7.4610c",
        "name": "test : message",
        "topic": "message",
        "payload": "",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "x": 206.25000953674316,
        "y": 648.7500019073486,
        "wires": [
            [
                "26579600.dc41da"
            ]
        ]
    },
    {
        "id": "a5142063.bd71e",
        "type": "comment",
        "z": "3ab980c7.4610c",
        "name": "Send IoT commands to Sense Hat LED Matrix",
        "info": "",
        "x": 276.25000953674316,
        "y": 488.75000190734863,
        "wires": []
    },
    {
        "id": "f8160c87.24af3",
        "type": "link out",
        "z": "3ab980c7.4610c",
        "name": "Main Dashboard",
        "links": [
            "29589c.35d02764",
            "812cb766.9d6458",
            "97ce57d3.0ee688"
        ],
        "x": 479.583327293396,
        "y": 196.80556106567383,
        "wires": []
    },
    {
        "id": "8a8775f1.72ea58",
        "type": "ibmiot",
        "z": "",
        "name": "BlueMix",
        "keepalive": "60",
        "domain": "",
        "cleansession": true,
        "appId": "",
        "shared": false
    },
    {
        "id": "9daa45bb.2be6c8",
        "type": "dashDB",
        "z": "",
        "hostname": "dashdb-entry-yp-dal09-08.services.dal.bluemix.net",
        "db": "BLUDB",
        "port": "50000",
        "name": "DashDB-STSA"
    }
]
```
1. Paste it into NodeRed, by clicking on the upper right menu (Three horizontal lines), the select import->Clipboard.
2. Paste the JSON that you copied into the center editor.
3. Click on the "new Flow" button.
4. Click on the "Import" button.
5. Double click on the **DashDB** node and change the Service name to the Name of your dashDB instance.
6. Double click on **IoT:Environment** node. Change "authentication" to **BlueMix Services** and then make sure the  **Device id** is set to **ALL**.
7. Double click on **IoT:Commands** node. Change "authentication" to **BlueMix Services** and then change **Device id** to **sensehat-xx** where xx is your team number assigned at the begining of the course.

## Add Table to DashDB
Copy the following text to your clipboad.

```
CREATE TABLE "SENSEDATA"
(


"SENSORID" VARCHAR(20),


"TEMPERATURE" DOUBLE,


"HUMIDITY" DOUBLE,


"PRESSURE" DOUBLE,


"TIMESENT" TIMESTAMP
);
```

1. To to the DashDB service from your BlueMix dashboard. Select open to start the DashDB admin page.
2. Once loaded click work with tables tile.
3. Click the **Add Table** button in the upper left.
4. Replace the sample DDL with the text you copied above, by pasting over the existng test.
5. Click **Run DDL**
6. You can close DashDB

## Update the Raspberry Pi NodeRed
This requires you to update the NodeRed instance running on the Raspberry Pi. Copy the text below and paste in your NodeRed Editor on the Pi.
```
This is the Pi
```
Make sure you have your IoT Foundation information which includes
- "OrganizationID"
- "DeviceType"
- "DeviceID"
- "Authentication Token".

1. Double click on the **Environment** node to open the details.
2. Click on the **pencil** icon on the credentials line.
3. Change the **OrganizationID** to the one you were assigned when you created the device in the IoT Foundation setup.
4. Click **Update**
5. Change the **DeviceID** to your "SenseHat-xxx" assigned number.
6. Click **Done**
7. Double click on **All Commands** node and change the **DeviceID** to your "SenseHat-xxx" assigned number.
8. Click **Done**
9. Click **Deploy**

## Watson Conversation Lab
This lab can be completed following the steps below.
1. Click the link [a relative link](wk2-wcs-workspace.json)
2. Triple click on the text that is very long line of JSON code. This could highlight all of the text. Copy the text and paste it into a text editor of you choice and save it as the same file name.
3. Start the Watson Conversation Workspace by clicking on the Watson Conversation service in your BlueMix dashboard.
4. Once you are in the workspace import the JSON file, by clicking on the import icon at the top of the workspace dashboard.
5. The screen should open to the newly created workspace.
6. The icon at the bottom of the list of icons on the left navigation will take you back to workspaces. Click the icon. You should see the "STSA-Lab" workspace.
6. Click the **3** buttons on the STSA-LAB tile. Then select view details. Highlight the WorkspaceID, copy it and then paste it in a temporary spot.
7. Click the link [a relative link](wk2-wcs-flow.json).
8. Copy the text and paste it into the NodeRed Editor. **Make sure to select "new flow" when importing.**
8. Double click on the **IOT: ColorChange**. Make sure the device ID is the proper value, something similar to "sensehat-xx".
10. Click done.
11. Double click on the STSA-CONV node. Change the workspace ID to the one you copied when the workspace was saved. Step 6 above.
12. Click done.
13. Click Deploy
14. Before the next step, copy the hostname of your NodeRed application. This is the hostname in the URL of your browser. Something like STSAWorkshops-xxx.mybluemix.net. You will need this for a future step. **Do not copy the "/red/..."** portion of the URL.
14. Click the link
[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/jdcalus/STSA-WCS-WebProxy.git)

15. When the BlueMix Devops page loads, click the **deploy** button at the bottom of the page.
16. Click the **Delivery Pipeline** tile.
17. Once the Deploy stage is completed, click on the **Rocket** icon. This will take you to your newly created application.
18. Click on the **runtime** link on the left. Then click the **Environment Variables** link in the center.
19. If you scroll down to the bottom you will see and entry for **Conversatin_URL**.
20. Paste your URL from step 15 into the entry field. **Make sure to keep the "/v1/workspaces...." information**.
21. Click Save.
21. Click the Overview link on the left navigation. You might have to wait for the application to restart.
22. Clik the **Visit APP URL** link.
23. You will get an error. Add **/webclient** to your URL and click enter.

You are done. Nice job

## Hybrid Cloud
Click the link  and copy the text. Paste it into a new flow in NodeRed
[Exercise 1 and 2](https://github.com/jdcalus/STSA-Workshop-3-Hybrid-Cloud/blob/master/completed-flows-part-1_2.json)

Click the link  and copy the text. Paste it into a new flow in NodeRed
[Exercise 3 - 5](https://github.com/jdcalus/STSA-Workshop-3-Hybrid-Cloud/blob/master/completed-flows-part-3.json)
In this flow, there two **http request** nodes. You need your weather company data credentials to update these nodes.
1. In the Bluemix dashboard, click on your Weather Company Data tile.
2. ON the left navigation there is a link for **Service Credentials**. Click the link.
3. Click the **view credentials** in the middle of the screen. You need to copy the username and password so you can update the "http nodes"
4. Go back to NodeRed and double click on the **http node**.
5. Click on the **use basic authentication** check box.
6. Paste your Weather Data username and password into the respective field.
7. Click **done**.
8. Do the same thing again for the other **https request** node.
9. Click **Deploy**


## Blockchain
Clik the link and copy the text. Paste it into a new flow in NodeRed.
[Node Red Flow](https://github.com/SweetJenn23/BlockchainLab/blob/master/completed-blockchain-flow.json)
