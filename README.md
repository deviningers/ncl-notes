 # NCL Notebook
> My National Cyber League Personal Notes so I can remember what weird commands I used and how they work

## Overall Suggestions
- Always double check the answer, being the only one bringing down team accuracy kinda sucks
- There are more and more online webapps that have these tools built in (just google it)
- If you are really stuck, it helps to dumb it down and/or try going at it from another angle
- Organize your time, the challenges get surprisingly easier when you have food in your belly and a good nights rest
- "Try harder"


## Stego
#### Commands
- view metadata:
```bash
exif  #or exif2
exiftool
```
- check file:
```bash
file
strings 
	#-n :length of string
	#-t x :view offset x=hex d=decimal
```
- pull things out of files:
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
foremost file.sus
	# Carves out embedded and appended files and dumps them to output
outguess -k "key string" -r path/to/file.jpg output.txt
zsteg file.png    
	# needs to be installed with $ gem install zsteg
stegsnow -C -p password path/to/file.png
stegcracker steg.jpg wordlist.txt
	# brute forces passwords using wordlists (takes a while) 
```
- Gross GUI programs:
	- Stegosuite
	- DIIT (Digital Invisible Ink Toolkit) 
	- OpenStego


#### Links
- another tool they use is sometimes is DIIT (Digital Invisible Ink Toolkit) - [DIIT](http://diit.sourceforge.net/)
- an online port of StegSolve which inlucdes 32 bit planes, RGBS values, and color palettes - [StegOnline](https://stegonline.georgeom.net/upload)
- Extra helpful collection of tools in docker image - [Stego-Toolkit](https://www.kitploit.com/2018/06/stego-toolkit-collection-of.html)

## Open Source Intelligence (OSINT)

- this is really just googling and going off hunches till you make it

#### Links
- How to google dork - (Wiki)[https://en.wikipedia.org/wiki/Google_hacking}
- this tool is useful to convert GPS coordinates / get location - [GPS-coordinates](https://www.gps-coordinates.net)
- online exif viewer (one of many) - [Exif](http://exif.regex.info/exif.cgi)
- Reverse image search:
	- [Google Images](https://images.google.com/)
	- [Tineye](https://tineye.com/)

## Enumeration & Exploitation

#### Links 
- Free programs for reverse engineering:
	- [Cutter](https://cutter.re/)
	- [Ghydra](https://ghidra-sre.org/)
- Online reverse engineering tool - [odaweb](https://onlinedisassembler.com/odaweb/)

## Log Analysis 
#### Commands
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
split -l x input.txt outputPrefix    # split file into smaller files after x lines  
```

#### Links
- [Grep regex](https://linuxize.com/post/regular-expressions-in-grep/)
- [Stole sum idea from here](https://askubuntu.com/questions/785038/how-can-i-sum-numbers-on-lines-in-a-file)
- [AWK is cool](https://www.howtogeek.com/562941/how-to-use-the-awk-command-on-linux/)


## Crypto 
#### Links
- Great crypto solveing website - [Cryptii](https://cryptii.com/)
- A crypto identifier w/ solvers - [boxentriq](https://www.boxentriq.com/code-breaking/cipher-identifier)
- Good for advanced algos - [CyberChef](https://gchq.github.io/CyberChef/)
- lots of solvers - [dcode](https://www.dcode.fr/tools-list)
- Cryptogram solver tool - [quipqiup](https://www.quipqiup.com/)
- another tool site - [rumkin](http://rumkin.com/tools/cipher/cryptogram-solver.php)


## Password Cracking
#### Commands
- identify hashes:
```bash
hashid path/to/file
hash-identifier
	# prompts for hash, w/ cool ascii art
```
- creating dictonary:
	- rockyou.txt is a good start to figure out if there's a pattern 
	- search google/github for premade lists eg: txt of all pokemon
	- wikipedia also has a lot of lists but they probably require cleaning
- crack hashes using hashcat (the cool way):
```bash
hashcat -m <hash mode> -a <attack type> hashes.hash dictionary [-r /usr/share/hashcat/rules/ruleset.rule] # use "--stdout" to print out guesses 
hashcat -m 0 - a 6 hash dict "?n?l?u?s?a" 	# to append mask to end
hashcat -m 0 -a 6 hash "?a?a" dict         	# to preppend mask to beginning
```
- make your own ruleset, or you can search for others on github
```bash
./mp64 -o output.rule "pass?a"
# will generate a rulelist of pass1, pass2, passA, pass!...
```
- The ***'easier'*** CPU intensive hash cracking tool, John The Ripper:
```bash
john hash.hash --wordlist=dict --rules:All	# Hail Mary
zip2john  					# pull hash out of encrypted zip (need to remore another part before using hashcat)
```

#### Links
- Identify hashes - [identifier1](https://hashes.com/en/tools/hash_identifier)
- Use this for ez password cracking - [CrackStation](https://crackstation.net/)
- When making a dictionary and you're too lazy to use a rule to switch characters - [ConvertCase](https://convertcase.net/)
- Hashcat instructions, or just read the man page - [Hashcat](https://hashcat.net/wiki/doku.php?id=hashcat)
- Hashcat ruleset creation help - [Rule Based Attack](https://hashcat.net/wiki/doku.php?id=rule_based_attack)
- An article discussing rulelists - [One rule to rule them all](https://notsosecure.com/one-rule-to-rule-them-all/)
- Practice w/ Defcon's hashlist - [Defcon 2020](https://github.com/62726164/cmiyc2020)
