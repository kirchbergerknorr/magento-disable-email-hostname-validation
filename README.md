# Magento Patch: Disable Email Hostname Validation

## Problem

Creation of Customer raising one of those errors:

- appears to be a DNS hostname but cannot match TLD against known list 
- appears to be a local network name but local network names are not allowed 

## Solution

There are new generic Top Level Domain extension (gTLDs). These are 
going to cause issues with Zend Validator. 

The best fix is to disable hostname validation in Magento and 
leave it up to the end user to correctly enter a domain name: 

find `Mage_Eav_Model_Attribute_Data_Abstract` and

change

    $validator = new Zend_Validate_EmailAddress();

to 

    $validator = new Zend_Validate_EmailAddress(array('domain'=>false));

Or you can simply install this patch via composer:

## Installation

*composer.json example*

```
{
    "minimum-stability": "dev",
    
    "repositories": [
        {"type": "composer", "url": "http://packages.firegento.com"},
        {"type": "git", "url": "https://github.com/kirchbergerknorr/magento-disable-email-hostname-validation"},
    ],
    
    "require": {
        "kirchbergerknorr/magento-disable-email-hostname-validation": "*"
    },
    
    "extra": {
        "magento-root-dir": "src"
    }
}
```

Read how to [Install Magento via Composer](https://medium.com/magento-development/magento-and-composer-44af0883abd9).

## Support

If you have any issues with this extension, 
open an issue on [GitHub](https://github.com/kirchbergerknorr/magento-disable-email-hostname-validation/issues/new).


## Contribution

Any contribution is highly appreciated. The best way to contribute code is 
to open a [pull request on GitHub](https://help.github.com/articles/using-pull-requests).

## Developer

Aleksey Razbakov
[@razbakov](https://twitter.com/razbakov)

License
-------
[OSL - Open Software Licence 3.0](http://opensource.org/licenses/osl-3.0.php)

Copyright
---------
(c) 2015 [kirchbergerknorr.de](https://kirchbergerknorr.de)
