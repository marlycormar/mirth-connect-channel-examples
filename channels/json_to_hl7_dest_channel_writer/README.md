## Description
This channel receives a `json` file over an `HTTP` request, transforms it into an `hl7` message, and sends it to another channel. Templates for both the `json` and `hl7` files are included.

    Source: HTTP Listener
    Source Transformer: json to hl7
    Destination: Channel Writer

## Setup
- Import the channel.
- Update the id of the destination channel.

## Usage
To send a message to mirth connect, use the following curl request:

    curl -H "Content-Type: application/json" --data @json_template.json 'http://127.0.0.1:8002/api/channels/<channel_id>/messages'

Note: `<channel_id>` must be substituted by the id of the current channel.




