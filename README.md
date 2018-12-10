# Implementing basic GFS in distalgo
<https://sites.google.com/a/stonybrook.edu/sbcs535/projects/gfs-distalgo>

Instructions to run the code:

It is recommeneded that the user should delete the directory ‘/tmp/gfs/chunks’ so that the files that were left from previous run gets removed.


To run main process:
	python3 -m da main.da

Main.da file was used for testing during our local development. It contains the message formats for the different operations that we support and a complete end to end flow with different operations. 

To run Correctness Testing:
	python3 -m da test.da <testCase Number> (testCases are numbered from 0-16)
	Example: python3 -m da test.da 4

TestCase Number mapping with TestCase (Negative test case means failure of operation and positive test case means operation  working as expected)

0 = Create - Negative Test Case
1 = Write -  Negative Test Case
2 = Delete - Negative Test Case
3 = Read - Negative Test Case
4 = RecordAppend - Negative Test Case
5 = Snapshot - Negative Test Case
6 = Create - Positive Test Case
7 = Write -  Positive Test Case
8 = Delete - Positive Test Case
9 = Read - Positive Test Case
10 = RecordAppend - Positive Test Case
11 = Snapshot - Positive Test Case
12 = End-To-End Testing (Create, Write, RecordAppend, RecordAppend, Snapshot, Snapshot, Read, Delete)
13 = End-To-End Testing - Multiple Reads (Create, Create, Write, Snapshot, Read, Read, Read, Read)
14 = End -To-End Testing (Create, Create, Write, RecordAppend, Snapshot, Read, Read, Delete)
15 = Consistency Testing -(Multiple Record Appends,Snapshot)
16 = Availability Testing - (Reading file before and after killing one of the chunkserver)


To run Performance Testing:
python3 -m da PerformanceTesting.da <NumberOfClients> <TestCaseNumber>

TestCase Number mapping with TestCase 

1 = This test case will create the user entered number of clients, create a single file, write a 670 character string to it and will try to read the same file from each of the created clients (N concurrent reads)
2 = This test case will create the user entered number of clients, create  user entered number of files, and try to write the 679 character string into each of the created file using each of the client created (N concurrent writes)
3 = This test case will create the user entered number of clients, create a single file, and append 670 character string into the same file from the user entered number of clients (N concurrent Record Appends)

Example: python3 -m da PerformanceTesting.da 500 2 → Running this command will run 500 concurrent Writes from 500 clients

Currently the chunkSize is 10. For running the performance test we recommend that for large clients we should increase the chunkSize. We need to set the same value of chunkSize in master.da and client.da
