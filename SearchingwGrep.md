# Topic 3.3 Searching with Grep Notes 
Use scopus.bib file to do grep searches
Use direct link and wget command to access: `wget https://raw.githubusercontent.com/Obakoush/OBICT690/main/scopus.bib`

## Snipit of data 

## Basic Commands
Grep searches line by line, `grep "^@" scopus.bib` will return lines starting w @
result :
```
@ARTICLE{Januário2024,
@ARTICLE{Pizelo202492,
@ARTICLE{Fabris2024,
@ARTICLE{Sauer2024,
@ARTICLE{Mu2024218,
@ARTICLE{Arnold20241,
@ARTICLE{Zhang2024,
@ARTICLE{Das202483,
@ARTICLE{Khalil20242204
```


Search for specfic word in title without case sensetivity (-i)

```
grep -i "Chess" scopus.bib
title = {Grandmasters, distinct elite: Taste submitted to discussion from the social conditioning factors of the predilection for chess}
title = {Improving ranking quality and fairness in Swiss-system chess tournaments}
title = {Checking gender bias: Parents and mentors perceive less chess potential in girls}
title = {Regulation of temperature distribution in fixed bed reactor for CO2 methanation through “CHESS” monolith structure catalyst}
title = {Minimum Number of Consecutive Rounds With Same Colour in a Chess Tournament}
title = {A modified chess knight reconfiguration approach for mitigating power losses in PV systems}
```
```
grep -i "Tournament" scopus.bib
	title = {Improving ranking quality and fairness in Swiss-system chess tournaments},
	title = {Minimum Number of Consecutive Rounds With Same Colour in a Chess Tournament},
```
Get a count of the matching lines for a specific term "Chess" w & w/o case sensitivity 
```
grep -c "Chess" scopus.bib
1
grep -ci "Chess" scopus.bib
6
```
`
Get journal titles 
```
grep "journal" scopus.bib
	journal = {International Review for the Sociology of Sport},
	journal = {Representations},
	journal = {Robotics},
	journal = {Journal of Quantitative Analysis in Sports},
	journal = {Geriatrics and Gerontology International},
	journal = {Journal of experimental psychology. General},
	journal = {Applied Thermal Engineering},
	journal = {Resonance},
	journal = {Energy Reports},
```
or search for journal titles that start w tab indent 
```
grep -P "\tjournal" scopus.bib
	journal = {International Review for the Sociology of Sport},
	journal = {Representations},
	journal = {Robotics},
	journal = {Journal of Quantitative Analysis in Sports},
	journal = {Geriatrics and Gerontology International},
	journal = {Journal of experimental psychology. General},
	journal = {Applied Thermal Engineering},
	journal = {Resonance},
	journal = {Energy Reports},
```
or search for journal titles that begin w "=" `grep "journal =" scopus.bib` to get same results

### Cut and Sed
- cut command (basic) is used to extract specific parts of each line. Divides each line into fields and returns the selected fields
- sed command (more complex) reads line by line, applies specfied command and outputs. Used for search & replace

Cuts "journal =" from each journal line 
```
grep "journal =" scopus.bib | cut -d"=" -f2
{International Review for the Sociology of Sport},
 {Representations},
 {Robotics},
 {Journal of Quantitative Analysis in Sports},
 {Geriatrics and Gerontology International},
 {Journal of experimental psychology. General},
 {Applied Thermal Engineering},
 {Resonance},
 {Energy Reports},
```
Cuts the journal, = , and {}, sed replaces the space and { from w nothing from each journal line to get cleaner list
```
grep "journal =" scopus.bib | cut -d"=" -f2 | \
    sed 's/ {//' | sed 's/},//' | \
    sort | uniq -c | sort

      1 Applied Thermal Engineering
      1 Energy Reports
      1 Geriatrics and Gerontology International
      1 International Review for the Sociology of Sport
      1 Journal of Quantitative Analysis in Sports
      1 Journal of experimental psychology. General
      1 Representations
      1 Resonance
```
Same command but with "title" instead of journal.
```
grep "title =" scopus.bib | cut -d"=" -f2 | \
>     sed 's/ {//' | sed 's/},//' | \
>     sort | uniq -c | sort

      1 A modified chess knight reconfiguration approach for mitigating power losses in PV systems
      1 Appl Therm Eng
      1 Checking gender bias: Parents and mentors perceive less chess potential in girls
      1 Connecting through clicks: A longitudinal examination of internet use and depressive symptoms among middle- and old-aged Chinese
      1 Energy Rep.
      1 Games and the Rise of Systems Thinking: From Models to Machines
      1 Geriatr. Gerontol. Int.
      1 Grandmasters, distinct elite: Taste submitted to discussion from the social conditioning factors of the predilection for chess
      1 Improving ranking quality and fairness in Swiss-system chess tournaments
      1 Int. Rev. Sociol. Sport
      1 J Exp Psychol Gen
      1 J. Quant. Anal. Sports
      1 Minimum Number of Consecutive Rounds With Same Colour in a Chess Tournament
      1 Playing Checkers with an Intelligent and Collaborative Robotic System †
      1 Regulation of temperature distribution in fixed bed reactor for CO2 methanation through “CHESS” monolith structure catalyst
      1 Representations
      1 Resonance
      1 Robotics
```
* note to self while this did produce titles, this command did not word since there are lines that include the journal tutles under them.

### Total Citations
- using grep & awk command summarize citation data
```
grep -o "Cited by: [0-9]*" scopus.bib | \
>     awk -F":" \
>     'BEGIN { printf "Total Citations: "} \
>     { sum += $2; } \
>     END { print sum }'
Total Citations: 1

```
formula breakdown:
- the `grep -o "Cited by: [0-9]*" scopus.bib` looks for # of times "Cited by:" followed by any number in file
- pipe `|:` pipes/passes grep output to awk command
- awk command `awk -F":":` Splits input w colon seperator
- the `'BEGIN { printf "Total Citations: "}:` prepends output w "Total Citations"
- the `{ sum += $2; }:` sums each citation count to total
- the `END { print sum }':` returns total sum
- output `Total Citations: 1`

## Reflection
When running `grep "journal" scopus.bib` I wanted to see if `grep "article" scopus.bib` would return article titles however with research I learned `grep -oP '(?<=title = \{).*(?=\},)' scopus.bib` is how you would get that. 



  
