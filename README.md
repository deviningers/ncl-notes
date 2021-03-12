# NCL Notebook
My National Cyber League Personal Notes so I can remember what weird commands I used and how they work

## Overall Notes
- always double check the answer, being the only one bring down team accuracy kinda sucks


## Stego
### Commands
- view metadata:
```bash
exif 
# or maybe exif2
exiftool
```
- check file:
```bash
type
file
strings [-n : length, -t x : view offset x=hex d=decimal]
binwalk 
	#checks for embedded files
	#-Me recursively extracts any files
steghide
```


### Tools
- this tool is useful to convert GPS coordinates / get location
[GPS-coordinates](https://www.gps-coordinates.net)
- another tool they use is sometimes is DIIT (Digital Invisible Ink Toolkit)
[DIIT](http://diit.sourceforge.net/)
- a great online tool 
