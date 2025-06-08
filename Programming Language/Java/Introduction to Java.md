# How Java Works
[[The Floyd-Warshall Algorithm]]
Java as we know it follows the “Write once, run everywhere” principle (WORA). The source code goes through a multiple of different stages of processing to the machine. 
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfgW2g-ff9dQIeexRODW9bxnQEe5B1MdLYgV6MeoM3SteB-vlciskGYr5DkonlaGyQekbIbyb5g82KLB_AizUf92qTvsvu22ET_24pGMVu4ZsDWvohSdDWjYZFW1c6DpVzGAO9Uuw?key=NYsBoIud9kfIR1KB4s1FEUXY)**

There are two key components here, the JDK and the JRE. 

The JDK (Java Development Kit) is behind all the development of Java programs. The JDK contains a compiler (javac), java development tools and the JRE (Java Runtime Environment). 

To run Java programs, a machine needs only the JRE to be installed. However, the JDK is required when the machine is used to write and compile Java code. So, JRE is not exclusive to JDK as it can be installed as a standalone package. 

What JDK has is the compiler (javac) that takes our .java source code and converts them into a bytecode (.class) file. The .class file will have the same name as that of the .java source file.  
For example - Hello.java -> Hello.class. 

This bytecode is recognizable by the JRE and it will go through some processing before running the code. We’ll not go into the details of the JVM and JRE architectures here as this is an overview of the process. But there’s a JIT (Just-in-time) compiler that works hand in hand with the JVM (Java Virtual Machine) and is a part of the JVM architecture. The reason being the JVM is an interpreter and not a compiler. 

Since interpreters are not time efficient, JIT converts the loaded bytecode into machine code. This accelerates the execution process. Otherwise JVM would’ve to interpret the same sequences inside the bytecode repeatedly (e.g. multiple function calls) which would result in a lengthy translation process. 

And finally we get native machine code for the targeted hardware the JRE is installed into. We can finally run the java program.

