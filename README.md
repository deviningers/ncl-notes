# NCL Notebook
> My National Cyber League Personal Notes so I can remember what weird commands I used and how they work

## Overall Notes
- always double check the answer, being the only one bring down team accuracy kinda sucks
- always make sure you know what section you are in before trying to answer


## Stego / OSINT
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
strings 
	#-n :length of string
	#-t x :view offset x=hex d=decimal
```
- pull things out of file
```bash
binwalk 
	# checks for embedded files
	#-Me :recursively extracts any files
steghide extract -sf picture.jpg
	# usually used with passwords but can work without
	#-sf :specify filename
pngcheck -vtpf picture.png
	#-v :verbose
	#-t :display text
	#-p :displays contents of optional chunks
	#-f :continue after major errors

```
### Tools
- this tool is useful to convert GPS coordinates / get location - [GPS-coordinates](https://www.gps-coordinates.net)
- another tool they use is sometimes is DIIT (Digital Invisible Ink Toolkit) - [DIIT](http://diit.sourceforge.net/)
- an online port of StegSolve which inlucdes 32 bit planes, RGBS values, and color palettes - [StegOnline](https://stegonline.georgeom.net/upload)
- Extra helpful collection of tools in docker image - [Stego-Toolkit](https://www.kitploit.com/2018/06/stego-toolkit-collection-of.html)

## Enumeration & Exploitation

## Log Analysis 

## Crpto 

## Password Cracking

