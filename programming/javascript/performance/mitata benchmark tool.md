---
created: 2024-09-30T12:11:50.449Z
updated: 2024-09-30T12:11:50.449Z
---
https://github.com/evanwashere/mitata

A benchmarking tool with very neat terminal graphics, and looks like lots of nice features.

```
-------------------------------------- -------------------------------
1 + 1                   318.11 ps/iter 325.37 ps         ▇   █         !
                (267.92 ps … 11.14 ns) 363.97 ps ▁▁▁▁▁▁▁▁█▁▁▁█▁▁▁▁▁▁▁▁
Date.now()               27.69 ns/iter  27.48 ns  █                   
                 (27.17 ns … 44.10 ns)  32.74 ns ▃█▂▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁

                        ┌                                            ┐
                  1 + 1 ┤■ 318.11 ps 
             Date.now() ┤■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■ 27.69 ns 
                        └                                            ┘

-------------------------------------- -------------------------------
Bubble Sort               2.11 ms/iter   2.26 ms  █                   
                   (1.78 ms … 6.93 ms)   4.77 ms ▃█▃▆▅▂▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁
Quick Sort              159.60 µs/iter 154.50 µs  █                   
               (133.13 µs … 792.21 µs) 573.00 µs ▅█▂▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁
Native Sort              97.20 µs/iter  97.46 µs        ██            
                (90.88 µs … 688.92 µs) 105.00 µs ▁▁▂▁▁▂▇██▇▃▃▃▃▃▂▂▂▁▁▁

                        ┌                                            ┐
                                        ╷┌─┬─┐                       ╷
            Bubble Sort                 ├┤ │ ├───────────────────────┤
                                        ╵└─┴─┘                       ╵
                        ┬   ╷
             Quick Sort │───┤
                        ┴   ╵
                        ┬
            Native Sort │
                        ┴
                        └                                            ┘
                        90.88 µs            2.43 ms            4.77 ms
```