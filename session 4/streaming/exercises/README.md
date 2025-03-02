# Working with streams 

- In this workshop, we will read TCP streams & Combine them together ([Spark TCP Stream](0.spark-tcp.py))
- Then we will perform come windowing compitations (count, average...) ([Spark TCP Window](1.spark-tcp-window.scala))

![spark stream](/res/img/spark-TCP-stream.png)

![random walk](https://miro.medium.com/max/4000/1*WABRtmAWBd0rmEOsbectRA.png)

- To that effect, the python script [SignalTCPSend.py](SignalTCPSend.py) is provided to you.   
  Take a minute or two to quickly skim through the code.  
  Focus mainly on the usage description
  
- Start with a frequency of 1 sec, and slide it up as you validate the complete stream chain 

- Advanced : to spice up the exercice, you could modify the script to send event time as well  
  along with the value (when you have time, maybe later).<br>
  This would illustrate the event time vs processing time paradigm.

- Split your terminal 

- In the first terminal launch 2 signal simulator commands :  
 ````
  python SendSignalTCP.py -p your_chosen_port_1_here -s 10&
  python SendSignalTCP.py -p your_chosen_port_2_here -s 10&
  ````
  
- in another terminal

- run a Spark Shell and execute the provided spark excerpts  
  to manipulate streams to produce the desired result  
  (port numbers should be changed according to what you feed the TCP script)
  
  YOU NEED TO REPLACE THE PORTS WITH YOUR CHOSEN PORTS FIRST

  ````
  pyspark --conf spark.ui.showConsoleProgress=false
  ````
  
  Setting the `showConsoleProgress` option to false frees the shell so we can get back the hand while streaming in the background. 
  (Otherwise it keeps pumping and doe not return the shell to the user)
  
  OR
  
 - run : `spark-submit spark-tcp.py`<br>
   
   YOU NEED TO EDIT THE PY FILE TO INSERT YOU CHOSEN PORTS FIRST

- Check that the output of the streams is written in the corresponding hdfs folders for each stream

- Explore the Spark Stream Web UI if you have the chance to do so.  
  
