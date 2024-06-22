# *CCSMB 14:* Stereo television

*Author: @WindClan*  
*Version: v1.0*  
*Last updated: 2024-06-22*  

## Both:
BIMG video should be at least 57x38 characters (resolution of a 3x3 monitor) and no more than 20 fps.

The only requirement for the video is that it can be decoded without hogging server resources

## Server:
Videos should either be in BIMG but other formats do not break compliance as long as they are marked in "type" to avoid issues with clients and there is an open-source encoder and decoder
  
  an example of this would be [PBB](https://raw.githubusercontent.com/craftytv/pigutv/main/pbbconverter.py) which is supported in the example server

High framerate broadcasts in BIMG should only use the default CraftOS pallete or a static pallete that doesn't change
  
Each frame of video should have enough audio to last the entire frame and no more

Each packet sent from the server most have "protocol" set to "stereovideo"

Each packet should have metadata for the TV broadcast

An optional feature that packets can have is subtitles by including a `subtitles` index in a frame

An example of a compliant server is [here](https://github.com/craftytv/television/tree/main/channel)

Example of a packet:
```lua
{
  protocol = "stereovideo", -- Always stereo video
  type = broadcastType, -- Image format (BIMG, etc.)   SHOULD BE ALL LOWERCASE
  audio = {
    left = leftbuffer, -- Decoded PCM, left channel
    right = rightbuffer -- Decoded PCM, right channel
  },
  video = currentFrame, -- Either a frame of PBB or BIMG
  subtitle = subtitle, --Subtitles is avaliable
  meta = {
    name = station, --TV station name
    title = program, --What the name of the video is
    owner = owner --Owner of the TV station
  }
}
```

## Client:
Clients should be able to display BIMG and avoid incompatible formats to prevent any issues

Supporting formats other than BIMG does not break compliance as long as there is an open-source encoder and decoder 

Clients should be able to play stereo audio in-sync with the frames

Clients should be able to display subtitles by reading the "subtitles" metadata from each frame

Displaying metadata (ex. station and program) attached to broadcasts is optional

If the client supports multiple palletes, the client should be able to switch back to default pallete before changing broadcasts

An example of a compliant client is [here](https://github.com/craftytv/television/tree/main/tuner)
