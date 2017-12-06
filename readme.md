# Resize On The Fly


CloudFormation template of resize on the fly. Used services include:
- S3
- Api Gateway
- CloudFront
- Lambda


**Features**

- Image resizing
- Quality optimizing - (jpeg only)

**How It Works**


This is your default url:

`http://{your_cdn}/image.jpg`

By adding `/w{}/h{}/q{}` parameters you will get the desired image on the fly

`http://{your_cdn}/w960/h540/q{}/image.jpg`

**Using The Template**

Upon creating the stack you will be asked to type an S3 bucket name and Api name. During the installation, it will download a node.js deployment package for your Lambda from TRT World.

**Usage**

`w{}` is for width

`h{}` is for height

`q{}` is for quality

`http://{your_cdn}/w960/h540/q90/image.jpg`

`http://{your_cdn}/w960/h540/image.jpg`

`http://{your_cdn}/w960/q90/image.jpg`

`http://{your_cdn}/w960/image.jpg`

Resizing focus is in the center of the image. What ever dimensions you want you will always get an image with desired dimensions. This might mean cropping of the image by zooming. Supported image containers are jpg and png.

**Possible Improvements**

- Extra querystring auth parameter to not allow unauthorized usage or abuse
- Use AWS Waff service for limiting number of requests
- Add a list of allowed resolution in Lambda code to prevent abuse usage of unwanted resolutions
- Add an error page in Lambda. You will redirect to this error page when ever something goes wrong with Lambda
- Enable Api Gateway cache to improve slight performance increase for error responses
- Usage other features of Sharp library. This template configured for basic usage. See doc for [Sharp](http://sharp.dimens.io/en/stable).

**Notes**

- By default we set Lambda memory to 640MB because we find it to be optimum setting for standard usage. It will be enough for 8k images.
- In Lambda you will find an environmental variable `cache_age` set to 86400(a day). You might want to change it to fit your needs.
- Sharp library doesn't support GIFs. You need to use additional library if you want resize on the fly to work on GIFs as well.



# Crop

CloudFormation template of resize on the fly. Used services include:
- S3
- Api Gateway
- Lambda

**Features**

- Image cropping

**How It Works**


You will send a post request to your Lambda's invoke url.

`POST https://{api_id}.execute-api.{your_region}.amazonaws.com/prod/crop`

Payload: `{"key": "image.jpg", "w": 100, "h":100, "x": 15, "y": 20}`

In response you will get cropped image link.

`{"url": "http://s3-{your_region}.amazonaws.com/{your_bucket}/image_1512560021767.jpg"}`

**Using The Template**

Upon creating the stack you will be asked to type an S3 bucket name and Api name. During the installation, it will download a node.js deployment package for your Lambda from TRT World.

**Usage**

`key` as string

`w` is for width as integer

`h` is for height as integer

`x` is for x coordinate as integer

`y` is for y coordinate as integer


Cropped image will be created with a timestamp

`image_1512560021767.jpg`


Crop coordinates start from top left of the image. Supported image containers are jpg and png.

**Possible Improvements**

- Configure Api Gateway to not allow unauthorized usage or abuse
- Add error handling in Lambda to get more helpful error responses for the users 


**Notes**

- By default we set Lambda memory to 640MB because we find it to be optimum setting for standard usage.
- Sharp library doesn't support GIFs. You need to use additional library if you want crop to work on GIFs as well.
- Usage other features of Sharp library. This template configured for basic usage. See doc for [Sharp](http://sharp.dimens.io/en/stable).

