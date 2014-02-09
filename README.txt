Python implementation of Lamport's Fast mutual and Bakery Algorithms
Date: 9/20/2013
by Madhurima Roy
--------------------------------------------------------------------------------------------------------------------------
GENERAL USAGE NOTES
---------------------

- Usage : python.exe main.py <number of threads> <number of requests>

- The code has been developed on Linux v 2.6.28-11 using Python 3.3.2.

- An example output file has been included showing the unfairness of Fast mutex and fairness of Bakery algorithm.

- There is a sleep of 5 secs between the run of Fast Mutex algorithm and Bakery algorithm.

- There are commented sleep statements in the code which can be enabled to improve the dynamicity of the thread execution.

- Global variables have been used as a shared resource amongst threads.

- The output between different threads may be interleaved when high number of threads are being run. Therefore, grepping and automated way of verifying/reading the outputs may produce false negatives. 

-------------------------------------------------------------------------------------------------------------------------

SUMMARY
---------

Notes on Common Implementation 

- Starts by taking the number of threads and number of requests from the user. All request are from a single pool, from which each thread picks a single rquest and serves it to the CS as per the algorithm. 

- The distribution is done in circular fashion.

- The thread when finished, comes back to check if there are any more requests in the pool. If so, then picks up to server it. 

- In this way all threads will start up simultaneously and keep serving requests from the pool until the pool gets empty.- The count of requests that have been served is maintained in shared variable, 'no_requests', inside the CS because this variable is shared amongst all the threads. 

- Also there is an entry section and exit section to the CS which has been used to synchronize the access to the CS by the threads.

Lamport's Fast Mutual Implementation
------------------------------------

- The program starts with calling the function 'thread_lamport_fast' with number of threads as argument. 

- sleep(1) is given for accumulating some threads. 

- The requests are circularly picked up by threads and served.

- Print convention used for the major actions are
	request for CS: "<thread#> Requesting CS"
	enterance of CS: "<thread#> Entering CS" 
	exit of CS: "<thread#> Exiting CS"


Lamport's Bakery Implementation
------------------------------------

- The program starts with calling the function 'thread_lamport_bakery' with number of threads as argument. 

- sleep(1) is given for accumulating some threads. 

- The requests are circularly picked up by threads and served.

- Print convention used for the major actions are
	request for CS: "<thread#> Requesting CS"
	token received: "<thread#> Received Token <token#>"
	enterance of CS: "<thread#> Entering CS"
	exit of CS: "<thread#> Exiting CS"

OUTPUT
-------
- There is no fairness in Fast Mutual algorithm.

- It is observed in Bakery's algorithm execution that the thread with the smallest token number gets into the CS first. Also, incase the token number is same, the thread with the smallest thread number gets more preference for CS.

------------------------------------------------------------------------------------------------------------------------
Observations
------------

1. In the beginning the implementation was not done with circular distribution of requests amongst threads. The output received was often observed to be in which first thread would finish all the requests and the rest of the threads that took time to get generated would just walk through the code. But in this surely the Fast Mutex would be jumbled and the Bakery would serve request as per  token. 

2. In order to prevent this unfairness in thread distribution, I implemented circular distribution for threads picking up requests. With this the order of the request being served might not be clear but it is being  more distributive towards threads.
-------------------------------------------------------------------------------------------------------------------------
