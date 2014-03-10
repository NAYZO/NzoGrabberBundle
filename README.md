NzoGrabberBundle
=====================

The **NzoGrabberBundle** is a Symfony2 Bundle used to Grabbe all types of links and URLs from any website.

Features include:

- Url Grabber for HTTP/HTTPS
- Url Grabber for HREF/SRC/IMG types
- Exclude any type of file by extension
- Prevent specified URLs from been Grabbed


Installation
------------

### Through Composer:

Add the following lines in your `composer.json` file:

``` js
"require": {
    "nzo/url-encryptor-bundle": "dev-master"
}
```

### Register the bundle in app/AppKernel.php:

``` php
// app/AppKernel.php

public function registerBundles()
{
    return array(
        // ...
        new Nzo\UrlEncryptorBundle\NzoUrlEncryptorBundle(),
    );
}
```

### Configure your application's config.yml:

The secret option in the configuration must contain a random key string of maximum 8 caracters and minimum of one caracter.

``` yml
# app/config/config.yml

nzo_url_encryptor:
    secret: YourSecretEncryptionKey 
```

Usage
-----

In your twig template use the filter to encrypt the variable in the url:

``` html

 <a href="{{path('my-path-in-the-routing', {'id': MyId | urlencrypt } )}}"> My link </a>

 # if it needed you can use the twig decryption filter:

 <a href="{{path('my-path-in-the-routing', {'id': MyId | urldecrypt } )}}"> My link </a>
``` 
In the routing.yml:

``` yml
# routing.yml

my-path-in-the-routing:    
    pattern: /my-url/{id}
    defaults: {_controller: MyBundle:MyController:MyFunction}

```

In the controller use the decrypt service on the encrypted 'id' comming from the routing:

```php
     public function indexAction($id) 
    {
        $MyId = $this->get('nzo_url_encryptor')->decrypt($id);

        //....

    }    
```

If it needed you can use the encryption service to encrypt your data:

```php
     public function indexAction() 
    {   
        $Encrypted = $this->get('nzo_url_encryptor')->encrypt($data);

        //....

    }    
```

License
-------

This bundle is under the MIT license. See the complete license in the bundle:

See [Resources/doc/LICENSE](https://github.com/NAYZO/NzoUrlEncryptorBundle/tree/master/Resources/doc/LICENSE)