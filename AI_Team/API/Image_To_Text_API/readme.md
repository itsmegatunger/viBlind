## API Documentations

### References

| HTTP Method |            Resource URL            |                                Notes                               |  Data Type |
|:-----------:|:----------------------------------:|:------------------------------------------------------------------:|:----------:|
|  POST, GET  |           /v1/api/predict          | Send an image want to recognize, return objects recognition texts  |    JSON    |
|     GET     | /v1/resoures/predict_images/<name> |            Return an recognized image with bounding box            | image/jpeg |

### Examples
Assume we have an ```dog-and-cat.png``` in local.

1. /v1/api/predict (POST, GET)

__Request:__ 
```
Header = {
    "content-type": "image/jpeg"
}

Body = {
    "image" : "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAg..."   // Encode image as base64 
    "name" :  "dog-and-cat.png"
}
```
__Response:__

```
{
    "predict": "['dog', 'cat']",
    "imageSize": "2200x760"
}
```

2. /v1/resoures/predict_images/<name> (GET)

GET: http://52.187.125.140:5000/v1/resoures/predict_images/dog-and-cat

And you will recieve an recognized image with bounding box.