# utl-output-win_7-cpu-and-memory-usage-to-csv-files-and-tables
Output win 7 cpu and memory usage to csv files and tables
    Output win 7 cpu and memory usage to csv files and tables

    github
    https://tinyurl.com/rcluqv3
    https://github.com/rogerjdeangelis/utl-output-win_7-cpu-and-memory-usage-to-csv-files-and-tables

    I believe you can get these stats by processid?

    Note win 7 "perfmon.exe"  provides extensive graphics and interactive oerformance reports.
    However I like the command line option.

    While your program is running

    https://www.datadoghq.com/blog/collect-windows-server-2012-metrics/

    https://github.com/rogerjdeangelis/utl-driving-all-your-cores-at-I00-percent-utilization-parallel-processing

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    EXAMPLE Metrics that are available

    https://www.datadoghq.com/blog/collect-windows-server-2012-metrics/

    CPU Metrics

    Get-WmiObject Win32_PerfFormattedData_PerfOS_Processor

    Property Name              Command

    PercentProcessorTime       Get-Counter -Counter "\Processor(*)\% Processor Time"
    ContextSwitchesPersec      Get-Counter -Counter "\Thread(_Total)\Context Switches/sec"
    ProcessorQueueLength       Get-Counter -Counter "\System\Processor Queue Length"
    DPCsQueuedPersec           Get-Counter -Counter "\Processor(*)\DPCs Queued/sec"
    PercentPrivilegedTime      Get-Counter -Counter "\Processor(*)\% Privileged Time"
    PercentDPCTime             Get-Counter -Counter "\Processor(*)\% DPC Time"
    PercentInterruptTime       Get-Counter -Counter "\Processor(*)\% Interrupt Time"


    EXAMPLE Memory metrics

    Get-WmiObject Win32_PerfFormattedData_PerfOS_Memory

    Property Name              Command

    AvailableMBytes            Get-Counter -Counter "\Memory\Available MBytes"
    CommittedBytes             Get-Counter -Counter "\Memory\Committed Bytes"
    PoolNonpagedBytes          Get-Counter -Counter "\Memory\Pool Nonpaged Bytes"
    PageFaultsPersec           Get-Counter -Counter "\Memory\Page Faults/sec"
    PageReadsPersec            Get-Counter -Counter "\Memory\Page Reads/sec"
    PagesInputPersec           Get-Counter -Counter "\Memory\Pages Input/sec"
    PercentUsage               Get-Counter -Counter "\Paging File(*)\% Usage"

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
      ___ _____   __
     / __/ __\ \ / /
    | (__\__ \\ V /
     \___|___/ \_/

    ;

    CPU Metric
    ==========

    d:\sys\cpu.csv

    PERCENT CPU UTILIZATION

    "CPU","PercentProcessorTime"
    "0","100"
    "1","82"
    "2","94"
    "3","99"
    "4","88"
    "5","88"
    "6","94"
    "7","100"
    "_Total","2"


    Memory Metric
    =============

    d:/sys/mem.csv

    CommittedBytes
      7655354368

    *    _       _                 _
      __| | __ _| |_ __ _ ___  ___| |_ ___
     / _` |/ _` | __/ _` / __|/ _ \ __/ __|
    | (_| | (_| | || (_| \__ \  __/ |_\__ \
     \__,_|\__,_|\__\__,_|___/\___|\__|___/

    ;


    CPU Metrics


    Obs    VAR23       VAR22                 VAR28                VAR31                     VAR32

      1    CPU         InterruptsPersec      PercentIdleTime      PercentProcessorTime      PercentUserTime

      2    0           1540                  93                   6                         0
      3    1           468                   99                   0                         0
      4    2           560                   99                   0                         0
      5    3           1084                  56                   50                        37
      6    4           976                   93                   6                         6
      7    5           1172                  93                   6                         6
      8    6           1012                  99                   0                         0
      9    7           320                   93                   12                        0
     10    _Total      7136                  91                   10                        6


    Memory Metrics
    ==============

     WORK.memXpo


       COL1                          COL2

       PSComputerName                E6420
       __GENUS                       2
       __CLASS                       Win32_PerfFormattedData_PerfOS_Memory
       __SUPERCLASS                  Win32_PerfFormattedData
       __DYNASTY                     CIM_StatisticalInformation
       __RELPATH                     Win32_PerfFormattedData_PerfOS_Memory=@
       __PROPERTY_COUNT              44
       __DERIVATION                  System.String[]
       __SERVER                      E6420
       __NAMESPACE                   root\cimv2
       __PATH                        \\E6420\root\cimv2:Win32_PerfFormattedData_PerfOS_Memory=@
       AvailableBytes                10104741888
       AvailableKBytes               9867912
       AvailableMBytes               9636mb
       CacheBytes                    231870464
       CacheBytesPeak                811880448
       CacheFaultsPersec             128
       CommitLimit                   34108264448
       CommittedBytes                7743967232
       DemandZeroFaultsPersec        208
       Description
       FreeAndZeroPageListBytes      4070612992
       FreeSystemPageTableEntries    33557000


    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;


    Open a command doc window (run as adminstartor?)

      1. > cd c:/windows/system32
      2. > powershell

      3. > Get-WmiObject Win32_PerfFormattedData_PerfOS_Processor | Select Name, PercentProcessorTime | Export-Csv -Path d:\sys\cpu.csv
      4. > Get-WmiObject Win32_PerfFormattedData_PerfOS_Memory | Select CommittedBytes | Export-Csv -Path d:\sys\mem.csv

      5. > Get-WmiObject Win32_PerfFormattedData_PerfOS_Processor | Export-Csv -Path d:\sys\cpuall.csv
      6. > Get-WmiObject Win32_PerfFormattedData_PerfOS_Memory | Export-Csv -Path d:\sys\memall.csv


    * MEMORY  STATS;

    dm "dimport 'd:\sys\memall.csv' work.memall";

    proc transpose data=work.memall out=memXpo;
    var _all_;
    run;quit;

    proc print data=memxpo(keep=col1 col2 where=(col1 ne ""));
    run;quit;


    * CPU STATS;

    dm "dimport 'd:\sys\cpuall.csv' work.cpuall";

    proc print data=cpuall(keep=var23 var22 var28 var31 var32);
    var var23 var22 var28 var31 var32;
    run;quit;



