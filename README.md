# flink-checkpointing-mechanism-for-fault-tolerance

This template demonstrating the checkpointing mechanism in Flink to achieve fault tolerance with a USE case. This Project has 1 Class to:-

[[CarSpeedLimitWithCheckpoint]] : class demonstrating the use case where on a particular highway if any car crosses the speed limit, the system will generate an alert message that `you crossing the speed limit and the average speed of few car that passed before you is [[this/55]] and show the car speed as well`. If a particular car is under speed limit, the message would be- 'Thank you for staying under the speed limit `65`, your current speed is [[this]] This is achieved by keeping a ValueState which has Tuple of 2 element- the count of cars passed and the summation of the speed of the cars passes right away. Here checkpointing is enabled with required configurations. If the application fails, on restarting it start from where it left off.

##How to Run- 
 1. Build the Jar of the application
 2. Go to the direactory where you installed Flink then run
   ./bin/flink run /home/Desktop/---.jar

   before running the application open the socekt connection.
   nc -l 9000
 3. Pass a tuple of higway name and speed of current car(highway is the key to aggregate)
    (NH-21,55)
    (NH-21,45)
 4. tail the log and see the message output
    tail -f log/flink-*-taskexecutor-*.out
 5. To test the fault tolerance Pass the speed of car other than double type
    (NH-21, e)
    pipeline breaks. reopen the socket connection and start sending the event. See the output. proceesing will aggregate from where it left off.
  
