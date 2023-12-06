# KAWS - Kernel aware warp scheduler and warp sharing mechanism
**Team members:** <br>
1.Vidyadhari <br>
2.Pranitha <br>
3.Tejonath <br>
4.Suresh <br>
5.Nishanth <br>

This project aims implementation of kernel aware warp scheduler and warp-sharing mechanism(KAWS) by doing changes in GPGPU-sim source code.<br>
The **kernel aware warp scheduler** is the new scheduler that should be created. The idea of implementation of this new scheduler is changing warp scheduling policy when the last cta in the kernel is detected to decrease the resource under utilisation and thus increases the performance.<br>
**Warpsharing mechanism** is to share operand collector units (OCUs) between warp schedulers to maximize the performance by maintaining pipeline and reducing pipeline stalls.<br>
## The observations are as follows:
## Total no.of gpu-sim cycles and ipc values
| **Benchmarks** | **scheduler type** | **cycle** |  | **ipc** |  |
| --- | --- | --- | --- | --- | --- |
|||with warpsharing|without warpsharing|with warpsharing|without warpsharing|
|pathfinder|KAWS|290449|289566|2148.4133|2154.9646|
||lrr|300284|296026|2078.0476|2107.938|
||gto|299631|298455|2082.5764|2090.7825|
|Hotspot|KAWS|37306|37078|2412.1931|2427.0264|
||lrr|39060|39216|2303.873|2294.7083|
||gto|37364|37221|2408.4487|2417.7019|
|bfs|KAWS|302957|297665|101.5453|103.3506|
||lrr|298272|297568|103.1403|103.3843|
||gto|298809|298603|102.9549|103.0259|

## stalls
| **Benchmarks** | **scheduler type** | **Pipeline stall** |  | **Idle** |  |**scoreboard stall** |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
||| with warpsharing | without warpsharing | with warpsharing | without warpsharing | with warpsharing | without warpsharing |
|pathfinder|KAWS|29837589|28791853|17199814|16935425|182776044|182428237|
||lrr|28279808|27766395|28781892|28124642|184493792|183586447|
||gto|29088557|28501735|18597084|18522897|184084266|183512016|
|Hotspot|KAWS|3482764|3406449|2392420|2411654|15879642|15603628|
||lrr|5359723|5221919|5871196|5965022|17154167|16920577|
||gto|263637384|3474096|3382815|3408190|15977062|15679695|
|bfs|KAWS|11671939|12108806|4665389|4680676|148360868|147768502|
||lrr|12567065|12206900|5162629|5160419|147418345|147334121|
||gto|2693871|12353888|4568337|4590569|147604384|147700573|

## % improvement observed with KAWS
| **Benchmarks** | **wrt lrr** | | **wrt gto** | |
|---|---|---|---|---|
||with warpsharing|without warpsharing|with warpsharing|without warpsharing|
|pathfinder|3.4|2.23|3.16|3.06|
|Hotspot|4.7|5.76|0.155|0.038|
|bfs|-0.55|-0.032|-0.37|0.3|

## Grpahs
