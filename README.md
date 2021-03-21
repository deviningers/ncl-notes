 # NCL Notebook
> My National Cyber League Personal Notes so I can remember what weird commands I used and how they work

## Overall Notes
- always double check the answer, being the only one bring down team accuracy kinda sucks
- always make sure you know what section you are in before trying to answer
- there are more and more webapps that have these tools built in


## Stego / OSINT
### Commands
- view metadata:
```bash
exif  #or exif2
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
### Links
- this tool is useful to convert GPS coordinates / get location - [GPS-coordinates](https://www.gps-coordinates.net)
- another tool they use is sometimes is DIIT (Digital Invisible Ink Toolkit) - [DIIT](http://diit.sourceforge.net/)
- an online port of StegSolve which inlucdes 32 bit planes, RGBS values, and color palettes - [StegOnline](https://stegonline.georgeom.net/upload)
- Extra helpful collection of tools in docker image - [Stego-Toolkit](https://www.kitploit.com/2018/06/stego-toolkit-collection-of.html)

## Enumeration & Exploitation

## Log Analysis 
### Commands
- Pull out column(s) based on designated fiter(s)
```bash
awk -F "seperator" '{commands $value}'
awk -F ";"     # -F allows you to specify the column splitter
awk -F " |:"   # filters based on both spaces and :'s
awk '{print $1 " and " $(NF)}'  # command prints "first column and last column"
awk '{n += $1}; END{print n}'   # sums up all $1 values and returns that value at the end 
```
- filter based on strings or regex
```bash 
grep
grep -i -v -c -o -r    # --ignore-case, -v --invert-match, --count, --only-matching, --recursive
grep -A NUM -B NUM     # --after-context, --before-context, prints NUM lines before or after grepped lines
grep "string" 'regex'  # single quotes is for regex and double quotes is strings
grep -E -o "(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)" file   # Real IP regex
```
- extra commands
```bash
wc        # word count, -l to count lines, -w to count words, -m to count characters, -c to count bytes
tr 	  # translate, -d 'char' to delete character, 
sort      # -n to sort by numeric values 
uniq      # -c to count occurances (needs to be sorted first)
```

### Links
- [Grep regex](https://linuxize.com/post/regular-expressions-in-grep/)
- [Stole sum idea from here](https://askubuntu.com/questions/785038/how-can-i-sum-numbers-on-lines-in-a-file)
- [AWK is cool](https://www.howtogeek.com/562941/how-to-use-the-awk-command-on-linux/)


## Crpto 
### Links
- Great crypto solveing website - [Cryptii](https://cryptii.com/)
- A crypto identifier w/ solvers - [boxentriq](https://www.boxentriq.com/code-breaking/cipher-identifier)
- Good for advanced algos - [CyberChef](https://gchq.github.io/CyberChef/)
- lots of solvers - [dcode](https://www.dcode.fr/tools-list)
- Cryptogram solver tool - [quipqiup](https://www.quipqiup.com/)
- another tool site - [rumkin](http://rumkin.com/tools/cipher/cryptogram-solver.php)

## Password Cracking

