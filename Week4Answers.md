# Week 4 Answers

Devin Comba
My VM was not responding, so I used Visual Studio Code on my own computer. 

1. Empty fields in each file and also the files differed in the size of the empty fields.

DB: Good observations. Were certain values missing entirely in some files?

2. Cleaning
    - find: `;`, replace: `\t`
    
    DB: Good.
    
    - find: `\t\t`, replace: `\tNaN\t`
    
    DB: Good! Does running this once fill all empty cells?
    
    - find: `( |\t)$`, replace: ``
    
    DB: Good, but you might add a + in case there's more than one space or tab.
    
    - find: ` `, replace: `_` on line 1
    
    DB: Good.
    
    - find: `^(NaN\t){16}\n`, replace: ``
    
    DB: Good. Only suggestion is that the number of times the pattern is repeated may vary across files.
    
    - find: `(?:\.\d)\d\d`, replace: ``
    
    DB: Good, but I think you'll need to include the captured text in the replacement string.
    
3. To put the header line in the file: grep MH_Time .\Strdln_Twater_090611-090828_corrd.csv > 2009Measurements.txt
    To put the data from all three data files into the new file: grep -rh "^2009.*" . >> .\2009Measurements.txt
    
    DB: Good!
    
4. Used the same type of command as in 3 to add header t the new file.
    To add lines w/o Nan: sed -r 's/^.*NaN.*//' .\Strdln_Twater_090829-091012_corrd.csv >>..\completeLakeTemps.txt
        for each data file 
        
    DB: Good.
        
5. To capture and put the 1st of the month measurements into new file: grep -rh '[0-9][0-9][0-9][0-9]-[0-9][0-9]-01' >> ..\SemiMonthlyLakeTemps.txt
    To capture and put 15th of the month measurements into new file: grep -rh '[0-9][0-9][0-9][0-9]-[0-9][0-9]-15' >> ..\SemiMonthlyLakeTemps.txt
    
    DB: Good.
    
6. To get measurements from midnight to 6am: grep -rh '^...........0[0-6]' . > NightTimeLakeTemps.txt
    To get measurements from 8pm to midnight: grep -rh '^...........2[0-4]' . >> NightTimeLakeTemps.txt
    
    DB: Very good. The pattern I used was much more complicated.
    
7.  awk '{print $3}' ./* >> depth_0.1m.txt

    DB: Good. You could also include the dates and times to keep them paired with the measurements.
