# flask-oauth2-server

An OAuth2 server implemented in [Flask] utilizing the [Authlib] library.

## Development

This project uses [pip-tools] for dependency management. To install all dependecies for development run:

```
pip-sync dev_requirements.txt requirements.txt
```

### SSL Options

There are two options for running this server in development.

#### Option 1. no TLS
 
If you are not concerned with SSL behavior in dev you can set the `AUTHLIB_INSECURE_TRANSPORT=1` environmental variable. Without transport level security(TLS) you will be exposing your headers and therefore any Bearer tokens to the world.

#### Option 2. Self signed certificates

Creating a self signed certificate with OpenSSL and using with the werkzueg dev server is relatively simple.

From your project folder:
```
mkdir keys
openssl req -x509 -newkey rsa:4096 -nodes -out ./keys/cert.pem -keyout ./keys/key.pem -days 365
```

Here we are creating a new certificate `cert.pem` with its corresponding private key `key.pem` and a validity date of 365. We placed this in a directory named `keys` at the root of our project folder and we have a .gitignore rule to prevent the keys from being uploaded to version control. 

Now when we run our werkzueg dev server we just need to specify the locations of the cert and key:

```
flask run --cert ./keys/cert.pem --key ./keys/key.pem
```

When you visit the URL in the browser add the certificate to the list of trusted certs and you will not be prompted by the browser safety features again.


## License and Attribution

This project builds off of the [Authlib] example server and therefore is distributed under the same BSD License.


[pip-tools]: https://github.com/jazzband/pip-tools
[Flask]: http://flask.pocoo.org/
[Authlib]: https://authlib.org/