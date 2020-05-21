![HumanBios](https://scontent.fjnb10-1.fna.fbcdn.net/v/t1.0-9/90850375_106333177684413_7143218645533982720_n.png?_nc_cat=105&_nc_sid=dd9801&_nc_eui2=AeHw9n-wQzRWM1tl4RHa-z7TWt8ItV6YmV9a3wi1XpiZX1nZnStF_Kv-paCt0Uygk0w&_nc_ohc=1I73K76FVpgAX_pNyB6&_nc_ht=scontent.fjnb10-1.fna&oh=d74c40338d48079aa970e3f88aa6aee7&oe=5EEB48D8)

# Humanbios-Documentation
This is system documentation for the HumanBios project

## Prerequisites
```
$ sudo apt-get install -y graphviz
$ sudo apt-get install python3-sphinx
$ git clone https://github.com/HumanbiOS/HumanBios-Documentation.git
```
Navigate to docs/build/html and open index.html

## Build
Add the necessary .rst files under docs/source and link them in index.rst toctree
```
$ cd docs
$ make html
```

## Need help?
https://www.sphinx-doc.org/en/master/index.html

