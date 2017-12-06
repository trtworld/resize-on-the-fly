**Resize On The Fly**


Cloudformation template of resize on the fly. Used services include:
- S3
- Api Gateway
- Cloudformation
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

Upon creating the stack you will be asked to type an S3 buket name and Api name. During the installation, it will download a node.js deployment package for your lambda from TRT World.

**Usage**

`http://{your_cdn}/w960/h540/q{}/image.jpg`

`http://{your_cdn}/w960/h540/image.jpg`

`http://{your_cdn}/w960/q{}/image.jpg`

`http://{your_cdn}/w960/image.jpg`

Resizing focus is in the center of the image. What ever dimensions you want you will always get an image with desired dimensions. This might mean croping of the image by zooming. 

**Possible Improvments**

- Extra querystring auth parameter to not allow unauthorize usage or abuse
- Use AWS Waff service for limiting number of requests
- Add a list of allowed resolution in lambda code to prevent abuse usage of unwanted resolutions
- Add an error page in lambda. You will redirect to this error page when ever something goes wrong with lambda
- Enable Api Gateway cache to improve slight performance increase in images with the same url
- Usage other features of Sharp library. This template configured for basic usage.

**Notes**

By default we set lambda memory to 640MB because we find it to be optimum setting for standard usage. It will be enough for 8k images.