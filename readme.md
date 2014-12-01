CryptoPPP Library Module For Processwire
========================================

Implements Steve Gibson's [PPP One-Time-Pad System](https://grc.com/ppp/design.html) along with some additional helpers.


Pre-requisites
----

Requires the mcrypt and bcmaths PHP extensions to be installed before the module will install properly.

On debian based systems you can install mcrypt as follows...

    # apt-get install php5-mcrypt mcrypt
    # php5enmod mcrypt


Generating A Single Key
----

Simply use ```$key = CryptoPPP::genKeys();``` or ```$key = CryptoPPP::genKeys(1);```


Generating Multiple Keys.
----

If you want 2 keys you would do ```$keys = CryptoPPP::genKeys(2);``` to get them in the $keys array or do ```list($k1,
$k2) = CryptoPPP::genKeys(2);``` to assign them to named variables.

Now that you have at least one key, you can use it as the basis of generating tokens or token streams.


Converting A Key Into A Token (a strings of characters).
----

The simplest way to convert a key into a token of a given length and using a given output alphabet is to call the
```CryptoPPP::keyToToken``` static method. If no length or alphabet is defined a 12 character token using the default
alphabet (```!#%+23456789:=?@ABCDEFGHJKLMNPRSTUVWXYZabcdefghijkmnopqrstuvwxyz```) will be created from the key.

To create tokens with a format such as 'X7gM-jA9v-KtWs' where the length of the 'blocks' and the 'glue' between them are
customisable you can use the related helper method ```CryptoPPP::keyToTokenBlocks()```.


Generating A Token Sequence (a One-Time-Pad) From A Key + Sequence Number.
----

If your application can associate an incrementing sequence number with a key, then you can use the PPP system to
generate a One-Time-Pad (a stream of tokens.)  This is simply done by passing the key, the sequence position, output
alphabet and token length to ```CryptoPPP::getCode()```. Once your application finishes using that token from the token stream, simply increment the sequence number ready for the next usage.
