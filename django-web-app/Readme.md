testing with 2 browers
log a user each

tod
lea
pw x2

source https://www.geeksforgeeks.org/realtime-chat-app-using-django/

    class ChatConsumer(AsyncWebsocketConsumer): Here we are creating a class named ChatConsumer which inherits from AsyncWebsocketConsumer and is used to create, destroy and do a few more things with WebSockets. And here we are creating ChatSocket for the required purpose.
    async def connect(self): This function works on the websocket instance which has been created and when the connection is open or created, it connects and accepts the connection. It creates a group name for the chatroom and adds the group to the channel layer group.
    async def disconnect(): This just removes the instance from the group.
    async def receive(): This function is triggered when we send data from the WebSocket ( the event for this to work is: send ), this receives the text data which has been converted into the JSON format ( as it is suitable for the javascript ) after the text_data has been received, then it needs to be spread out to the other instances which are active in the group. we retrieve the message parameter which holds the message and the username parameter which was sent by the socket via HTML or js. This message which is received will be spread to other instances via the channel_layer.group_send() method which takes the first argument as the roomGroupName that to which group this instance belongs and where the data needs to be sent. then the second argument is the dictionary which defines the function which will handle the sending of the data ( “type”: “sendMessage” ) and also dictionary has the variable message which holds the message data.
    async def sendMessage(self, event): This function takes the instance which is sending the data and the event, basically event holds the data which was sent via the group_send() method of the receive() function. Then it sends the message and the username parameter to all the instances which are active in the group. And it is dumped in JSON format so that js can understand the notation. JSON is the format ( Javascript object notation)
