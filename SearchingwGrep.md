# Topic 3.3 Searching with Grep Notes 
To do:
- Go through learn-the-cli in 3.1 - done
- Go through learn-the-filesystem in 3.1 - done
- Go through flashcards in 3.1 - do again on wed
- Do the grep walkthrough this week

   **Notes for 3.3 Grep**
I decied on using chess as a search term for scopus database
I have typed in the command to upload my files to g cloud a bunch of times and keep getting this error
`wardah@main-ubuntu1:~$ 
ERROR: (gcloud.compute.scp) Could not fetch resource: Request had insufficient authentication scopes.`

I updated the system and rebooted byt I am struggling to figure out how to avoid this error. (I ended up finding solution on element)
- solution:
  `wget https://raw.githubusercontent.com/Obakoush/OBICT690/main/scopus.bib`

`wardah@main-ubuntu1:~$ grep "journal" scopus.bib
	journal = {International Review for the Sociology of Sport},
	journal = {Representations},
	journal = {Robotics},
	journal = {Journal of Quantitative Analysis in Sports},
	journal = {Geriatrics and Gerontology International},
	journal = {Journal of experimental psychology. General},
	journal = {Applied Thermal Engineering},
	journal = {Resonance},
	journal = {Energy Reports},`

  I need to go through the commands once again for practice
  




  
