# render-with-both-cpu-and-gpu--KdenLive-FIX
This is to fix the GPU render times taking Longer in most cases (That i have experinced).
Why have it an option at all to render with your GPU if the encoding has to pass through the cpu anyways ?...
Well that is what is going on when you do try; thus due to the backend applecation "Melt" and how
it likes to go about prossesing your video and or audio project. What we are doing here is 
letting Melt know to not just use 1 thread or 1 core to encode , to instead use the given value. ect. 


I will be making this file compatable with all numbers of cores , but for now I just need 
it for what im doing . Expect update soon!



this is the Files Location within the source code:

/kdenlive-master/src/dialogs





Bellow is the section of the deep within the (renderwidget.cpp) file. All i did was change the condition 
Count < 2    to    Count < 1 
Then
threadCount = 2; to  threadCount = 24 ;


    int threadCount = QThread::idealThreadCount();
    if (threadCount < 1 || !m_view.parallel_process->isChecked() || !m_view.parallel_process->isEnabled()) {
        threadCount = 24;
    } else {
        threadCount = qMin(4, threadCount - 1);
    }


What im sure this is saying is if the value of SYS Ideal threads is over value 1 then expect to encode / use 
24 threads.

What ill be adding and messing around with is to see if thats true , if so i will add a config for each vlue of 
sys cores a user could have .


