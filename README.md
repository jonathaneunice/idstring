idstring
========

Python module to create alpha-numeric serial number strings with a check digit, with smart incrementing.

class IDstring generates (and checks) alphanumeric serial number strings with a checksum

It has been tested on Python 2.7 and Python 3.3.

It extends the built-in Unicode (str on Python 3) class using an __ADD__ method which accepts the integer ONE.
Adding 1 to an instance of the class will generate a new instance with an incremented value (and a new checksum).

So, in short, you can generate serial numbers like this:

    serial = idstring.IDstring(seed='1Y3R9C')
    while serial.startswith('1'):
        serial += 1
        print(serial)

With a result ending in:

>1YYYYVA

>1YYYYW8

>1YYYYX6

>1YYYYY4

>200000X

Incrementation flows smoothly through the alphabet -- "9" increments to "A". Incrementing "Y" gives "0" and 
causes a carry to increment the next digit. If you run out of digits, a "1" is prepended to the string.

The "Luhn mod N" algorith will add another digit (from the same alphabet) as a check digit.

The routine will automatically skip over patterns which contain substrings matching a list of "Dirty Words."

You can over-write the supplied alphabet and objectionable word lists.

You may supply an optional call-back function to assist in maintaining the persistence of the serial number
sequence of multiple program runs.

The Luhn-N check digit will detect any single character substitution, any inversion of adjacent characters
(except the first and last character in the alphabet: i.e. 0<->Y for the supplied default) and most other errors.

The default alphabet consists of [0-9] and [A-Y] dropping "I", "O", and "Q". The total of 32 symbols means
that it also can operate as a binary to base-32 converter (Like Hexadecimal but with 5-bit binary subfields).

Provision is made for a fixed subfield (of user defined length) between the check digit and the incrementing
field, so that multiple sites can produce non-overlapping series of numbers.  This subfield and the check digit
are included in the "dirty word" checking.

Installation uses the usual Python method:

    cd your-unzipped-directory
    python setup.py install


