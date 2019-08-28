# Exiv2 metatag extractor

`metaparser` is a CLI tool to parser and extract tag information from the metadata header of images. The tool organises a directory based on the list of tags extracted.

## Setting up the environment

The tool is written in `Python3` and its dependencies are listed in `requirements.txt`. I'd recommend using `virtualenvs` and `pip` to set this up:

```
$ virtualenv myenv --python=`which python3`
$ source myenv/bin/activate.sh
$ pip install -r requirements.txt
```
## Usage

The tool provides inline help by using the `-h` flag:

```
$ ./metaparser -h

usage: metaparser [-h] [-m MINIMUM] [-o OUTPUT] [-v] [-p] directory

positional arguments:
  directory             source folder with photos to be parsed.

optional arguments:
  -h, --help            show this help message and exit
  -m MINIMUM, --minimum MINIMUM
                        set the minimum number of photos for a tag to be
                        proceesed.
  -o OUTPUT, --output OUTPUT
                        create one folder per tag with all photos inside
  -v, --verbose         increase verbosity level
  -p, --print           print out the list of tags and photos on stdout.
```

The `directory` parameter is mandatory and specifies the directory which contains all images to be parsed. Once set, we can print out the tags founds and the number of images for each of them:

```
$ ./metaparser --print ~/Photos

castle (1) ['/home/anavarro/Photos/CAST_0.jpg']
vehicle (1) ['/home/anavarro/Photos/VEH_1.jpg']
(...)

```

In case we want to process only on the most interesting ones, we could set a minimum of images per tag:


```
$ ./metaparser --print --minimum=5 ~/Photos

beach (5) ['/home/anavarro/Photos/SZG_0.jpg',
           '/home/anavarro/Photos/SZG_1.jpg',
           '/home/anavarro/Photos/SZG_2.jpg',
           '/home/anavarro/Photos/SZG_3.jpg',
           '/home/anavarro/Photos/SZG_4.jpg']
(...)
```

Finally, it's possible to create a new folder structure with the extracted tags (the `-v` flag provides some extra information on stdout):

```
$ ./metaparser -v --minimum=5 --output=Outpout ~/Photos 

Copying  /home/anavarro/Photos/VIE_1.jpg Output/leisure
Copying  /home/anavarro/Photos/VIE_1.jpg Output/food
Copying  /home/anavarro/Photos/VIE_1.jpg Output/mountain
Copying  /home/anavarro/Photos/SZG_0.jpg Output/waterfall
(...)
```


