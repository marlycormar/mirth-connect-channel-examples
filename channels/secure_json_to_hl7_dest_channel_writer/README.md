## Description
This channel is functionally  a copy of the json_to_hl7_dest_channel_writer channel. It receives a `json` file over an `HTTP` request, transforms it into an `hl7` message, and sends it to another channel. Templates for both the `json` and `hl7` files can be found in **Channels > json_to_hl7_dest_channel_writer > templates**. However this channel also responds to HTTP requests and implements basic HTTP Authentication.

    Source: HTTP Listener
    Source Transformer: secure json to hl7
    Destination: Channel Writer


## Setup
- Import the channel and deploy it.
- Optional: change/add the credentials external applications need. To do this edit the Channel, go to **Source**, and change the **HTTP Authentication settings**. By default, the credentials are 

        Username: REDCap
        Password: 12345

## Usage
To send a message to mirth connect, use the following curl request:

    curl -H "Content-Type: application/json" --data @json_template.json -u <username>:<password> 'http://127.0.0.1:8002/api/channels/<channel_id>/messages'

For example:

    curl -H "Content-Type: application/json" --data @json_template.json -u REDCap:12345 'http://127.0.0.1:8002/api/channels/d4073467-0a37-45fc-a763-d9b5c379d4bc/messages'


Note: `<channel_id>` must be substituted by the id of the current channel. Also, this curl request is sent from localhost. If you are trying to send a message from an external machine you must replace 127.0.0.1 with the IP of the machine hosting the containers. This may be different from the host's public IP address for virtual machines. For example in Vagrant you will need to run `netstat -rn` to find the appropriate IP.
