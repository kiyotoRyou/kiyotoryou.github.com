---

layout: post
categories: [Hadoop]
tags: [Hadoop , Eclipse , Debug]

---

If you want to learn a open source project,there's maybe two good ways to achieve your goals.First is to communicate with the committers even  better with chair of the project.If this way is difficult to you,perhaps  tracing and debugging the source code is the perfect method.

Some programmers do this work by adding some log info to the source code,but when you had not family enough with the project,it's not a wise choice.
To set breakpoints and debug step by step will make you mind more clear.

Follow the three steps as follows,you can debug Hadoop source code in Eclipse easily.

###Step 1. Configure environment variable
In order to configure the hadoop's main thread to be intercepted by a debugger, you may need to configure the environment variable "`HADOOP_OPTS`" with the debugging information.
	
The environment variable "HADOOP_OPTS" will be captured by any execution from "`/bin/hadoop`" command, and therefore, you may only execute it when submitting a Hadoop command.The option interested for you to debug the job on Eclipse is the "`address=5000`". *Change the port number as your preference.* The option "suspend=y" tells the JVM to suspend its execution until a debugger have been attached to the executing job at the given port number.

####Running the command in the terminal :

> hadoop@master:$ export HADOOP__OPTS="agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5000"

####verifying its value

> hadoop@master:$ echo $HADOOP_OPTS
> agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5000
> == Starting the Suspended Hadoop MapReduce Job"

###Step 2. Running the hadoop command
After you have configured the HADOOP_OPTS environment variable,first start you hadoop cluster and you can have a test  using the regular command. For instance, try running the `hadoop fs -ls` as follows:

    hadoop@master:/hadoop/bin/$ hadoop fs -ls
    Listening for transport dt_socket at address: 5000

###Step 3. Configuring Eclipse

In order to debug the job, you must have created a hadoop source-code Project in Eclipse workplace. Once you have the source-code without compilation problems, you may add a remote debugger.

Going to the Eclipse main menu "*Debug -> Debug Configurations -> Remote Java Applications*". Change the name of the debugger on top of the screen and add the chosen port number. 



Once you click in the button "Debug", the debugger will be attached to the Hadoop thread you have submitted and the execution of the code will continue.

From this point on, the execution of the job will be suspended in the face of any breakpoint you have added into you classes.
 
