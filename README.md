Parallel-Transcode
==========

A script that can Parallel-Transcode the file.

单机并行转码单个文件。

Still in Alpha, not for production use! Please send me report, whether or not this is working. Thanks in advance.

Alpha测试，不适合生产环境。请发送报告，无论是能跑还是不能跑。谢谢。


Why?
--------
Yes, this was a issue back in 2012, and now in 2015, both ffmpeg and x264 had solved this problem properly in their code - You are able to ultimate your CPU, regardless how may cores you have.

But things are different when it comes to AVS. 

Right now, AVS is still in x86, and during the report from multiple users of Maruko Toolbox, no doubt AVS is the bottleneck of the speed: One with a E3-1230v3 may need to tun 3 instances to ultimate the usage of CPU. Another report from a Dual-E5-XXXX user said he had to run **10** instance at a time to run at a proper speed. That's insane.

祖传多线程，专治AVS。希望能解决高端CPU挂AVS不得不多开的问题。


Usage
--------

Python 2.7+ffprobe+ffmpeg+whatever-you-want

    python multi-ffmpeg.py (-h/help) (-i/input-file) (-s/slicer)
                           (-c/converter) (-q/queue-length)
                           (-a/arguments) (-f/full_command)
                           (-d/delete-temp) (-t/segment-time)
    
    -h: Default: None
        Print this usage file.
    
    -i: Default: None
        The input file.
        Please make sure it can be read by ffmpeg.
        
    -s: Default: 3
        The thread number of Slicer that cut the file into loseless pieces.
    
    -c: Default: 3 
        The thread number of Converter that convert the file into pieces.
        
    -q: Default: 10
        Max pieces.
    
    -a: Default: None
        The arguments you want to pass to ffmpeg when encoding.
        
    -f: Default: None
        In case you want something special, just input whatever command you want here!
        To make sure the command can be read,
        use {INPUT_SEGMENT_FILE}, {OUPUT_SEGMENT_FILE} in the command line.
        
    -d: Default: 1
        If set to 0, Parallel-Transcode will not delete any temporary files.
        1: Only delete at the end of stage.
        2: Delete on the fly.
    
    -t: Default: 30
        The time of one segment in sec.
           
    -v: Default: (Blank)
        The temporary file's format.
        If set to "avc", Parallel-Transcode will use a *loseless* way to transcode file to reserve its quality.
        It not set, the temporary file would be in MPEG2, same quality. There's no guarantee that this is loseless.
        
    -r: Default: 15
        Used with "-v avc".
        The crf to use when convert.
        0 for loseless.
    
    -n: Default: 0
        Dry run.
        Convert first N piece to test whether the script is running properly.

License
----

GPL v3.

是的，你看见了，请开源。

Misc
----

* 晚上写的，肚子饿了，有问题谅解，也没做PEP-8，随便看看吧。
* 代码很糟糕，我会尽可能redo，当然更欢迎pull request。
* 禁止转载到**墙内**各种电子公告服务（包括但不限于百毒贴吧、AC 丧尸岛、各种论坛、微博等）。发现腿打折.
* 只在OSX下测试，没有系统测试。Win上缺乏测试结果。/Only tested under OSX 10.10.1, and there's no test under Windows!
* CN101964894B专利帮我理清了一些思路。https://www.google.com/patents/CN101964894B?cl=zh 

History
----
0.04: Able to do a test dry run.

0.03: Add another mode of making cache file to reach quicker speed(6X on my machine, 13-late MBP).

0.02: Fix queue length.

0.01: The very first start
