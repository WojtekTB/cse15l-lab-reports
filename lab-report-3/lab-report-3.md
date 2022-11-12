Vadim Victor Kim  
CSE 15L  
11/09/2022

# Lab Report 3

## **Researching Commands**
I will be researching the `grep` command.  
When looking online I found following 3 ways of using this command.
 - `grep -i`
 - `grep -v`
 - `grep -R`

Following examples are ran inside of `technical` directory that can be found in [this](https://github.com/ucsd-cse15l-f22/docsearch/) repository.

 ## "`grep -i`" -> Case sensetivity

 Adding a `-i` option to your `grep` search removes the case sensetivity requirement from the search.  
 For example, lets say you want to find mentions of 'method' in the meth research document in order to quickly find the place where the methods of application.  
 If we simply run the command without the `-i` tag we can ensure that we are not gonna miss any parts where the method is described just because it was at the beginning of the sentence (i.e. started with a capital letter).
 ```
 grep -i 'method' ./government/Env_Prot_Agen/1-3_meth_901.txt
Tests recommended for use in this methods manual may be
static non-renewal or static renewal. Individual methods specify
 ```

Or for example if we are looking for 'aqueous outflow' mentions in the biome documents:
```
grep -i 'aqueous outflow' ./biomed/1471-213X-1-3.txt  
aqueous outflow. The primary source of aqueous is blood
```

Or if we are for example looking for a name of a specific person within the document and we are conserned that their name might have been capitalized inconsistently:
```
grep -i 'mckim' ./government/Env_Prot_Agen/1-3_meth_901.txt
McKim (1977) evaluated the data from 56 full life cycle
```

## "`grep -v`" -> Inverted search
Sometimes you are not looking for any specific instance of a word, but instead places where something is not present.

For example lets say we are working on the biomed file and we want to just find parts that do not include what causes 'disease':
```
grep -v 'disease' ./biomed/1471-213X-1-3.txt
        Background
        Abnormal anterior segment development is often
        associated with elevated intraocular pressure (IOP), an


        (...I will contract this for clarity...)

          in situ end-labeling of fragmented
          DNA (using BODIPY fluorophores, Molecular Probes, Eugene,
          Or.) and detection of condensed chromatin (with the
          dimeric cyanine dye YOYO-1, Molecular Probes) was used to
          analyze all of these sections [ 59]. Samples were
          analyzed with a confocal microscope and cells were
          identified as apoptotic only when they were double
          labeled. The occurrence of PCD was evaluated in the iris,
          ciliary body and TM.
```

Or if we trying to ignore lines that involve some person mentioned:
```
grep -iv 'mckim' ./government/Env_Prot_Agen/1-3_meth_901.txt
2.1 INTRODUCTION


2.1.1
The objective of aquatic toxicity tests with effluents or
pure compounds is to estimate the "safe" or "no-effect"
concentration of these substances, which is defined as the
concentration which will permit normal propagation of fish and
other aquatic life in the receiving waters. The endpoints that have

(...I will contract this for clarity...)

local, state and Federal rules and regulations. It is extremely
important that these rules and regulations be known, understood,
and complied with by all persons responsible for, or otherwise
involved in, performing toxicity testing activities. Local fire
officials should be notified of any potentially hazardous
conditions.
```

or if we are trying to not see lines mentioning stabbings in this 911 report collection:
```
 grep -v 'stab' /Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-2.txt
            THE FOUNDATION OF THE NEW TERRORISM
            A DECLARATION OF WAR
            In February 1998, the 40-year-old Saudi exile Usama Bin Ladin and a fugitive Egyptian
                physician, Ayman al Zawahiri, arranged from their Afghan headquarters for an Arabic

(...I will contract this for clarity...)

                Ladin said that the World Islamic Front for jihad against "Jews and Crusaders" had
                issued a "crystal clear" fatwa. If the instigation for jihad against the Jews and
                the Americans to liberate the holy places "is considered a crime,"he said,"let
                history be a witness that I am a criminal."
```
## "`grep -R`" -> Look through all files in directory

 Sometimes you want to just find mentions of something in multiple files in a directory. For times like these `-R` tag is perfect as it allows you to just run one command for multiple files.

 ```
 grep -R 'stab' /Users/vadimkim/Documents/GitHub/docsearch/technical/911report
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-13.4.txt:                killed there). KSM claims that Ramzi Yousef visited the NGO's establishment in
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-13.4.txt:                name of a guesthouse Bin Ladin established in Afghanistan for mujahideen recruits.
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-13.4.txt:                establishes rules for grand jury secrecy.

(...I will contract this for clarity...)


/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-10.txt:                    of what the armed forces call "security and stability operations."
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-11.txt:                created fresh sources of instability and new challenges for the United States.
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-11.txt:                established a new strategic assessments branch during July 2001. The decision to add
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-11.txt:            We can therefore establish that at least some government agencies were concerned
/Users/vadimkim/Documents/GitHub/docsearch/technical/911report/chapter-11.txt:                apparent than in the military establishment. After the August 1998 missile strike,
 ```

 looking up person's name:
 ```
 grep -Ri 'mckim' ./government/Env_Prot_Agen
./government/Env_Prot_Agen/ctf1-6.txt:McKim (1977) evaluated the data from 56 full life-cycle
./government/Env_Prot_Agen/1-3_meth_901.txt:McKim (1977) evaluated the data from 56 full life cycle
 ```

 or some other general information like chemical mentions:
 ```
 grep -iR 'chem' /Users/vadimkim/Documents/GitHub/docsearch/technical/government/Alcohol_Problems
/Users/vadimkim/Documents/GitHub/docsearch/technical/government/Alcohol_Problems/Session2-PDF.txt:undertaken using clinical impression or biochemical tests is not as
/Users/vadimkim/Documents/GitHub/docsearch/technical/government/Alcohol_Problems/Session2-PDF.txt:Other biochemical markers such as mean corpuscular volume, platelet
/Users/vadimkim/Documents/GitHub/docsearch/technical/government/Alcohol_Problems/Session2-PDF.txt:problematic con-sumption.45-50 Biochemical tests other than BAC may
/Users/vadimkim/Documents/GitHub/docsearch/technical/government/Alcohol_Problems/Session4-PDF.txt:environments. Research that examines pricing schemes and marketing
 ```