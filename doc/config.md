```
backend_emailOptions__from
```

- always put `backend_` first
- then each level of config should be seperate with a double underscore: `__`
- see `.backendrc-example` on the master branch for the config requirements

below are the common environments variables you should want to set:


### Mail sending

```
backend_emailTransport__service         Mailjet
backend_emailTransport__auth__user      your Username (or API key)
backend_emailTransport__auth__pass      your password (or Secret Key)
```


backend_emailTransport__service is for [nodemailer-wellknown](https://www.npmjs.com/package/nodemailer-wellknown) configuration  


### from email adress


```
backend_emailOptions__from              Email Builder <emailbuilder@backend.com>
```

### MongoDB database

the path to your mongoDB instance

```
backend_database                        mongodb://localhost/backend
```

### Admin password

```
backend_admin__password                 a password of your choice
```

### Hostname

The domain name of your app

```
backend_host                            backend-test.herokuapp.com
```

### AWS S3

Those are the keys you should set for aws

```
backend_storage__type                   aws
backend_storage__aws__accessKeyId       20 characters key
backend_storage__aws__secretAccessKey   40 characters secret key
backend_storage__aws__bucketName        your bucket name
backend_storage__aws__region            region of your bucket (ex: ap-southeast-1)
```

###### getting AWS id

[console.aws.amazon.com/iam](https://console.aws.amazon.com/iam) -> **create new access key**

###### creating the bucket

[console.aws.amazon.com/s3](https://console.aws.amazon.com/s3) -> **create bucket**

you have also to set the good policy for the bucket:

**Properties** -> **Permissions** -> **Add bucket policy**

and copy and paste this:

```json
{
	"Version": "2008-10-17",
	"Statement": [
		{
			"Sid": "AllowPublicRead",
			"Effect": "Allow",
			"Principal": {
				"AWS": "*"
			},
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::YOURBUCKETNAME/*"
		}
	]
}
```

then replace `YOURBUCKETNAME` by your real bucket name


### Branding 

You can define here the main colors of the application:

- **contrast** colors are for the text laying upon the associated background-color
- **primary** is for the top navigation
- **accent** is for the buttons and links

```js
"brand": {
    "color-primary": "rgb(233,30,99)",
    "color-primary-contrast": "white",
    "color-accent": "#3f51b5",
    "color-accent-contrast": "white",
    "name": "ESET"
},

```

### Other config

```js
// will print on the front some debug infos
debug:          false,
// redirect any http request to https
forcessl:       false,
images: {
  // needed only if not using S3 image storage
  uploadDir:    'uploads',
  // tmp directory name for image upload
  tmpDir:       'tmp',
  // cache resized images & add cache-control to image request
  cache:        false,
},
```
