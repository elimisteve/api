# Gifs API Documentation [![](https://img.shields.io/badge/API-online-brightgreen.svg)](https://api.gifs.com)

The gifs API makes it dead simple to convert and transcode a vast array of media into our HTML5 optimized gifs.com player, a compressed .gif, .webm and .mp4.

Send us any `.gif`, `.mp4`, `.webm`, `giphy`, `imgur`, `gfycat`, `streamable`, `instagram`, `twitter`, `facebook`, or `vine` links and we transcode your media lightning fast and serve it up in our awesome gifs player :zap:.

#### Can I see an example?

[Example get request](http://api.gifs.com/media/import?source=https://zippy.gfycat.com/LimpingEveryHairstreak.webm&title=ClapClapClap) - try switching out the `source` with a vine link!

## Media Routes

The media routes allows anyone to add short media from various sources including external URLs and uploading from disk. There is a `150mb` size and `30s` time limit for all media being added. We support converting the following file mime types: `image/gif`, `video/mp4`, `video/webm`.

### Import Endpoint `https://api.gifs.com/media/import`

Import media that's already available online with the `/import` endpoint. You can also link directly to a `giphy`, `imgur`, `gfycat`, `streamable`, `instagram`, `twitter`, `facebook`, or `vine` web page instead of the actual the source file and we'll automagically find the best quality to import.

Send a `POST` request with the following schema as `content-tye: application/json`:

| Parameter       | Type         | Required?  | Description                          |
| -------------   |--------------|------------|--------------------------------------|
| source          | string       | required   | The source URL of the media to add   |
| title           | string       | optional   | The title of the media               |
| tags            | []string     | optional   | The tags relating the the media      |
| nsfw            | boolean      | optional   | If the media is not safe for work    |
| attribution     | object       | optional   | Any attribution you want displayed   |

Attribution object schema is:

| Parameter       | Type         | Required?  | Description                                 |
| -------------   |--------------|------------|---------------------------------------------|
| site            | string       | required   | twitter, reddit, instagram, or a custom URL |
| user            | string       | optional   | The username for social media sites         |
| url             | string       | optional   | The url if site != social media             |

#### Example Request

```HTTP
POST /media/import HTTP/1.1
Host: api.gifs.com
Token: beta-access-token-monty
Content-Type: application/json
Accept: application/json
Accept-Charset: utf-8
{
 "source": "http://i.imgur.com/WUYpq61.gif",
 "title": "Cat does a front flip",
 "tags": ["cat", "flipping", "cat flip", "amazing cats"],
 "attribution": {
   "site": "twitter",
   "user": "gifsCom"
 }
}
```

#### Example Response

```HTTP
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8
{
 "success":{
    "page": "https://gifs.com/gif/wpk4Lw",
    "files": {
        "gif": "https://j.gifs.com/wpk4Lw.gif",
        "jpg": "https://j.gifs.com/wpk4Lw.jpg",
        "mp4": "https://j.gifs.com/wpk4Lw.mp4",
        "webm": "https://j.gifs.com/wpk4Lw.webm"
    },
    "oembed": "https://gifs.com/oembed/wpk4Lw",
    "embed": "<iframe src='https://gifs.com/embed/wpk4Lw' frameborder='0' scrolling='no' width='309' height='291' style='-webkit-backface-visibility: hidden;-webkit-transform: scale(1);' ></iframe>",
    "meta": {
        "duration": "2.61s",
        "frames": "26",
        "height": "291",
        "width": "309"
    }
 }
}
```

### Upload Endpoint `https://api.gifs.com/media/upload`

Upload media by sending a `POST` `multipart/form-data` request with the following form fields:

| Parameter         | Type      | Required?  | Description                                 |
| ------------------|-----------|------------|---------------------------------------------|
| file              | file      | required   | The file being uploaded                     |
| title             | string    | optional   | The title of the media                      |
| tags              | []string  | optional   | The tags relating the the media             |
| nsfw              | boolean   | optional   | If the media is not safe for work           |
| attribution_site  | string    | optional   | twitter, reddit, instagram, or a custom URL |
| attribution_user  | string    | optional   | The username for social media sites         |
| attribution_url   | string    | optional   | The url if site != social media             |

#### Example Request

```shell
curl \
  -F "file=@/media/gifs/awesome.gif" \
  -F "title=The most awesome gif eva" \
  -F "tags=awesome, cool, fun, gnarly" \
  https://api.gifs.com/media/upload
```

#### Example Response

```HTTP
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8
{
 "success":{
    "page": "https://gifs.com/gif/2k9BMv",
    "files": {
        "gif": "https://j.gifs.com/2k9BMv.gif",
        "jpg": "https://j.gifs.com/2k9BMv.jpg",
        "mp4": "https://j.gifs.com/2k9BMv.mp4",
        "webm": "https://j.gifs.com/2k9BMv.webm"
    },
    "oembed": "https://gifs.com/oembed/2k9BMv",
    "embed": "<iframe src='https://gifs.com/embed/2k9BMv' frameborder='0' scrolling='no' width='640' height='360' style='-webkit-backface-visibility: hidden;-webkit-transform: scale(1);' ></iframe>",
    "meta": {
        "duration": "4.104s",
        "frames": "123",
        "height": "360",
        "width": "640"
    }
 }
}
```
# FAQs

#### I just made something cool with the gifs API!

Feel free to send a pull request! If it's awesome, we'll merge it into our [examples](https://github.com/gifs/api/tree/master/examples).

#### What are you adding next!

:wink: You'll have to watch the gifs API to see our public releases.

#### Can I help or contribute, or pretty please see a sneak peak?

Oh - yes! We'd love to get some feedback. Please feel free to [get in touch with us](mailto:rory@gifs.com).
