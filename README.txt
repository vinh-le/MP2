README - MP1 Responses
*** All source code can be found in the SRC folder ***
*** Project files were compiled using IntelliJ but source code Java files should run in any system ***
----------------------------------------------------------------------------------------------
Part 1: Control Flow Analysis
I concluded that the given implementation for doAnalysis() was correct. I came to this conclusion by
locating the corresponding dominator analysis in the Soot source code (in the provided GitHub link).
I compared the two algorithms line-by-line and found them to be identicical in implementation.
----------------------------------------------------------------------------------------------
Part 2: Data Flow Analysis

CHA Output:
<src.Example: src.Animal selectAnimal()> may call <src.Cat: void <init>()>
<src.Example: void main(java.lang.String[])> may call <src.Example: src.Animal selectAnimal()>
<src.Example: void main(java.lang.String[])> may call <src.Cat: void saySomething()>
<src.Example: void main(java.lang.String[])> may call <src.Fish: void saySomething()>
<src.Animal: void <init>()> may call <java.lang.Object: void <init>()>
<src.Cat: void <init>()> may call <src.Animal: void <init>()>
<src.Cat: void saySomething()> may call <java.lang.System: void <clinit>()>
<src.Cat: void saySomething()> may call <java.io.PrintStream: void println(java.lang.String)>
<src.Cat: void saySomething()> may call <java.lang.Object: void <clinit>()>
<src.Fish: void saySomething()> may call <java.lang.System: void <clinit>()>
<src.Fish: void saySomething()> may call <java.io.PrintStream: void println(java.lang.String)>
<src.Fish: void saySomething()> may call <java.lang.Object: void <clinit>()>
Total Edges:12

PTA Output:
<src.Example: src.Animal selectAnimal()> may call <src.Cat: void <init>()>
<src.Example: void main(java.lang.String[])> may call <src.Example: src.Animal selectAnimal()>
<src.Example: void main(java.lang.String[])> may call <src.Cat: void saySomething()>
<src.Animal: void <init>()> may call <java.lang.Object: void <init>()>
<src.Cat: void <init>()> may call <src.Animal: void <init>()>
<src.Cat: void saySomething()> may call <java.lang.System: void <clinit>()>
<src.Cat: void saySomething()> may call <java.lang.Object: void <clinit>()>
Total Edges:7

Analysis:
The results showed that CHA found 12 total edges while PTA found 7 edges. This discrepency comes
from the fact that CHA is less precise; it gets all the subtypes of the object type, in this case
Animal, and any type that has a matching function definition is identified. These bring up false positives.
Dog, Fish, and Cat all have saySomething() methods, and each is returned as a counted edge. 
Some type of innacuracy is inevitable since the problem of pointer analysis is undecidable and cannot
be perfectly solved. The given example program that is being tested is very small, so the difference
in speed is less apparent. However, in larger cases, while less precise, the CHA approach will run faster
due to its near linear time complexity.
-------------------------------------------------------------------------------------------------
Part 3: Tracing Heap Accesses

TestSootLoggingHeap.java Output:
Thread Thread-14 wrote static field <src.HelloThread: int x>
Thread Thread-13 read instance field <src.HelloThread$TestThread: int y> of object Thread[Thread-13,5,Soot Threadgroup]
Thread Thread-14 read instance field <src.HelloThread$TestThread: int y> of object Thread[Thread-14,5,Soot Threadgroup]
Thread Thread-13 read static field <src.HelloThread: int x>
Thread Thread-14 wrote instance field <src.HelloThread$TestThread: int y> of object Thread[Thread-14,5,Soot Threadgroup]
Thread Thread-13 read static field <java.lang.System: java.io.PrintStream out>
Thread Thread-13 wrote static field <src.HelloThread: int x>
