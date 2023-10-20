https://github.com/red-data-tools/YouPlot

available with `brew install youplot` or `pip install youplot`. Here's the example from [[A bar graph in the terminal with gnuplot]], which looks much nicer than the gnuplot example:

```
$ cat /usr/share/dict/words | grep -o ...$ | sort | uniq -c | sort -r | head |
  uplot bar -d ' ' --fmt yx
       ┌                                        ┐ 
   ess ┤■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■ 9271.0   
   ion ┤■■■■■■■■■■■■■■■■■■■■■■■■ 6916.0           
   ous ┤■■■■■■■■■■■■■■■■■■■■■■ 6421.0             
   ing ┤■■■■■■■■■■■■■■■■■■■ 5539.0                
   ate ┤■■■■■■■■■■■■■■■■ 4561.0                   
   ble ┤■■■■■■■■■■■■■■■ 4351.0                    
   tic ┤■■■■■■■■■■■■■■ 3996.0                     
   ism ┤■■■■■■■■■■■■ 3485.0                       
   ist ┤■■■■■■■■■■■ 3286.0                        
   ite ┤■■■■■■■■■■■ 3061.0                        
       └                                        ┘ 
```