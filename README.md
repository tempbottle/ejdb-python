Embedded JSON database library Python 2.7/3.x binding
============================================================

Installation
---------------------------------

**Required tools/system libraries:**

* gcc
* **Python >= 3.x|2.7.x**
* EJDB C library **libejdb** ([from sources](https://github.com/Softmotions/ejdb#building) or as [debian packages](https://github.com/Softmotions/ejdb#ubuntu))

**Python binding published:** http://pypi.python.org/pypi/pyejdb

**(A) Installing using pip**

`pip` for python3 or python2 should be installed (`sudo apt-get install python3-pip` | `sudo apt-get install python-pip`)

```
umask 022

   sudo pip install pyejdb

Upgrading:
   sudo pip install pyejdb --upgrade
```

**(B) Installing directly from sources**

```
umask 022

git clone https://github.com/Softmotions/ejdb-python.git
cd ./ejdb-python
sudo python3 ./setup.py install
```


**(C) Installing on Ubuntu/Debian (only for Python3.x)**

```
sudo add-apt-repository ppa:adamansky/ejdb
sudo apt-get update
sudo apt-get install python3-ejdb
```


One snippet intro
---------------------------------

```python
import pyejdb
from datetime import datetime

#Open database
ejdb = pyejdb.EJDB("zoo", pyejdb.DEFAULT_OPEN_MODE | pyejdb.JBOTRUNC)

parrot1 = {
    "name": "Grenny",
    "type": "African Grey",
    "male": True,
    "age": 1,
    "birthdate": datetime.utcnow(),
    "likes": ["green color", "night", "toys"],
    "extra1": None
}
parrot2 = {
    "name": "Bounty",
    "type": "Cockatoo",
    "male": False,
    "age": 15,
    "birthdate": datetime.utcnow(),
    "likes": ["sugar cane"],
    "extra1": None
}
ejdb.save("parrots2", parrot1, parrot2)

with ejdb.find("parrots2", {"likes" : "toys"},
          hints={"$orderby" : [("name", 1)]}) as cur:
    print("found %s parrots" % len(cur))
    for p in cur:
        print("%s likes toys!" % p["name"])

ejdb.close()
```

