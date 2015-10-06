### HW3_CSCI5828


                     SOFTWARE ENGINEERING   -    HOMEWORK 3

<p><b>1. Using the material that we have covered in Lectures 8, 9, and 10, explain why the broken program doesn't work. What concurrency-related problems are occuring in this program? If you see the program end in livelock, then describe what is happening with the threads. Why can't they make progress? If you see the program end in another way, such as getting to the point where it prints out the product ids but doesn't include all of them, explain why you think that happened. Note: If you start to add printlnstatements to the Producers and Consumers, you may actually altar the behavior of the program! If you observe this, then also include a discussion on why that happens as well. In your answer, if you want to include snippets of code and/or output to explain what you are seeing, then do so. Use all of Markdown's capabilities to display what you need to explain the concurrency-related problems that you are observing.</b></p>

<p>The program given is a concurrent program as it involves multiple threads running simultaneously. They may or may not run in parallel.We have an unwanted behaviour from the program because there are multiple threads which try to access the shared data at the same time. </p>

This sharing of the same resource be problem surfaces when a shared data is accessesy some  by threads simultaneously at the same time is called. This is also known as the race condition.

The threads fail to adhere to the mutual exclusion property and thus the program produces unusual output where in some threads read the same variable when another thread try to write into that variable.

Here, in the given code, when we run it we come across many abnormalities such as the following

The word “Queue empty” is printed continuously at times. This is because, the productionLine Linkedlist is empty without any products in it and hence when the consumer threads tries to consume the products in the linked list, it prints Queue empty.

The sentence “Too many items in the queue” is produced when the products gets produced continuously and there are no Consumer thread to consume them.

2) Now switch your attention to the broken2 program. The only difference between the two programs are the synchronized keywords on the methods contained in ProductionLine.java. For this question, explain why this approach to fixing the program failed. Why is it that synchronizing these methods is not enough. What interactions between the threads are still occuring that cause the program to not be able to produce the correct output? Again, you may use snippets of code and/or output to illustrate your points. The only requirement for this question is that you focus exclusively on issues related to why this particular approach fails to solve the problem. In other words, your answer to this question should be different than your answer to the question above where you are discussing the program and its concurrency problems in general.

In the code implementation given in the folder Broken2, the only change is that, in the productionline file, the methods have been synchronized using the keyword “synchronized”. 

Using the keyword synchronized on a method, makes the thread acquire a lock on the method so that no other thread can enter that critical section and make changes to the objects and variables inside.


Even though the methods are synchronized there exists some abnormalities but the product id’s printed are somewhat consistent. This is because, the methods in Productionline are accessed by the Producer and Consumer threads through the productionline object-’queue’ which is not synchronized. 

Since this object is not synchronized, the threads are not able to see the recent updations made using this object. Hence the abnormality is seen with partial consistency. 

Once we synchronize the object of productionline - ‘queue’ in both the Producer.java and Consumer.java files, the product id’s are printed from 0 to 199 without showing any abnormal behaviour.


The queue - object of productionline has been synchronized in the file Consumer.java using syntax synchronized(queue) as shown in the below 


 
The queue - object of productionline has been synchronized in the file Producer.java using syntax synchronized(queue) as shown in the below.


