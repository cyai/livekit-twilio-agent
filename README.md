# Livekit Twilio Demo

The demo assistant use:

-   Deepgram for Speech-to-text
-   OpenAI for LLM and Text-to-speech

## Prerequisites

-   Phone number on one of the SIP Trunk providers: Here Twilio

-   A LiveKit server running, we can use the LiveKit [cloud](https://cloud.livekit.io/) or [self host](https://docs.livekit.io/realtime/self-hosting/local/) it.

-   Install LiveKit CLI:

    ```bash
    # on macOS
    brew install livekit-cli

    # on Linux
    curl -sSL https://get.livekit.io/cli | bash

    # on Windows
    winget install LiveKit.LiveKitCLI

    # from source
    git clone github.com/livekit/livekit-cli
    make install
    ```

## Run

### Setup and activate a virtual env:

`python -m venv venv`

`source venv/bin/activate`

### Set environment variables:

```bash
export LIVEKIT_URL=<your LiveKit server URL>
export LIVEKIT_API_KEY=<your API Key>
export LIVEKIT_API_SECRET=<your API Secret>
export DEEPGRAM_API_KEY=<your Deepgram API key>
export OPENAI_API_KEY=<your OpenAI API key>
```

### Install requirments:

`pip install -r requirements.txt`

### Run the agent worker:

`python minimal_assistant.py download-files`

`python minimal_assistant.py dev`

## Configure Twilio Trunk:

You need to Configure SIP to bridge phone calls to LiveKit rooms. You can follow the blog here: [Twilio SIP Trunking with LiveKit](https://docs.livekit.io/sip/quickstart/)

-   Once you have the SIP trunk setup, you need to populate the `outboundTrunk.json` file with the SIP trunk ID, authentication that you created in Twilio credentials list, termination uri and the Twilio phone number you want to use.

-   After that, you can run the `outboundTrunk.py` file to create the outbound trunk in LiveKit.

    ```bash
    lk sip inbound create inboundTrunk.json
    ```

- After running the above command you will get the `SIPTrunkID`, use that to populate the `sipParticipant.json` file. Use the phone number you want to use to get call from the assistant.

-   Run the `sipParticipant.py` file to create the SIP participant in LiveKit.

    ```bash
    lk sip participant create sipParticipant.json
    ```


