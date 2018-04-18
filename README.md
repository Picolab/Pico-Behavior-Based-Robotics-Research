# Pico-Behavior-Based-Robotics-Research
CS497R research

# Project Proposal 
Pico engine is an emerging rules engine used for solving IoT problems. My proposed research is
exploring the pico engine’s capabilities as a behavior based robot platform. The pico engine excels at extracting
logic and state into a single place called persistent compute objects(pico). Pico’s have the qualities needed for
behavior based computing which is reactive persistence. Recent research has demonstrated successful control
of general purpose input/output of a raspberry pi with the pico engine. If the pico engine is able to support
behavioral based logic, meaningful robots will be able to be constructed on top of the pico engine. While this
proposed research is driven for robotics application, a behavioral based Iot system would allow a smart house
to exhibit A.I. while allow integrations of other API’s and A.I.’s.
I propose extending the pico engine to control a robotics simulator like gazebo. Once the pico engine is able
to interface with a simulator, development of behavioral based logic can be driven by simulation.
Research strategies.
1. Read behavior based robotics research publications
2. Integrate pico engine with a simulator
3. Develop strategies for pico behavioral computation

# Final Report
Abstract
-----------
Previous research on using the Pico engine as a robotic programming platform showed great promise. This research explored the potential of the Pico engine as robotic platform.
The strategy was to investigate Behavioral Based Robotics (BBR) design pattern with the Pico Engine in mind. BBR is a commonly used approach to programming robotics which express organic like behavior. The ambitious goal was to implement a behavioral based program in the Pico-Engine to control a Gazebo simulated robot through a Robot Operating System (ROS) control layer. Using ROS control layer allows the Gazebo simulated robot to be replaced with a physical robot.

BBR investigation
-----------------------
Subsumption architecture is the idea that programs can be decomposed into sub component programs which are not restricted in a single logic flow but levels of operation. It’s from this idea that BBR emerged.  Where a behavior is a subprogram that’s expressed by certain sensor readings.  When behaviors compete for expression an arbiter decides which behavior should be expressed. We found the Pico engine could be used with subsuption architecture, where each level of abstraction would be a Pico and every component of that layer would be KRL rulesets. Arbiters would be first class actors represented as Picos between each layer. Each layer would interact by event channels where the previous layer would be treated as sensor data or event generators. 

BBR Emotion
-----------------
During research in subsumption architecture the idea of what kind of arbiters could be written came up. It’s this question that led to the thought “what if behavior arbitration was emotion based?”.  This would allow a smart house to exhibit a personality. Making it more than a smart house, a social robot.  Investigating this idea lead to hour glass of emotion (http://sentic.net/hourglass-of-emotions.pdf). The hour glass of emotion quantifies emotion into a single value or color, which would allow an arbiter to deterministically pick behaviors to be expressed.  While exploring this idea we found that emotion based arbitration could be used to overcome the domain transfer problem of machine learning. Currently we can train a neural net with in a single domain of data very efficiently, but lack the ability to transfer across problem domains. If you used emotion based arbitration to pick between neural networks trained on different domains of problems, the entire system would overcome the problem that a single neural net could not.  While advances in neural network training will quickly age the subsumption structure, its noteworthy of the power the system offers. 


ROS investigation
-----------------------
ROS targets to standardize the general programing of robots. The system has evolved to be very similar to the Pico engine. The Pico-engine enables the creation of PICO (persistent compute objects) and facilitates a sub domain for each Pico to receive events on. ROScore does essentially the same thing, starting a mater node that provides registering and naming new nodes as well as tracking subscribers and publishers. ROS’s master allows seamless communication between nodes.
The pico-engine has a UI for interacting with the engine and visualizing Pico systems.  The equivalent in ROS would be a set of command line tools. Rosgraph command line tool is used to visualize ROS node graph.  The ROS command tools provide all the functionality to ROS master that Picos UI does to the Pico-engine.  The Pico engine only has a few command line tools for managing scheduled events, so an admin could disable a scheduled event that is breaking the engine. The Pico engine command line tool for this only works while the engine is shut down.  While this has been sufficient, the Pico engine could benefit from a live command line tool for primitive features of the engine.
ROS is centered around code, system encapsulations and seamless communication of those systems. The Pico Engine is centered around giving things a digital Identity. Because of this difference ROS has solved problems the Pico engine has not yet addressed. 
For example, the idea of a collection is still being developed in the Pico engine, ROS has solved this idea with the concept of Topics. Topics are what Picolabs call an Event Router Pico or collection of Picos. Topics is a Message Generator that a node can subscribe too.
In ROS topics are associated with events or messages. Queries or method calls between nodes is called services. The Pico engine as the same functionality except for Rosparam. Rosparam is a standardized way to ask a function or module what parameters are expected. This allows a developer to write a ROS system that could be flexible to changes in different nodes. The pico-engine does this a little, when a developer shares and provides a testing map for the testing tab in the UI to use. 

Obstacles  
-------------
To seamlessly integrate the Pico engine with ROS there are a few obstacles that must be addressed.
ROS has defined event structure called messages used over subscriptions.  The Pico engine has the idea of subscriptions and secure messaging over subscriptions but lack explicitly defined events over subscription.  The Pico engine approaches this problem with channel policies, but policies lack key benefits of structured events ROS calls messages.  
 ROS messages are published at a certain frequency called hertz. The Pico engine supports scheduled events which could be used to simulate a frequency, but in general does not have the concept of representing event frequency as hertz.  This is directly correlated to a modification the engine needed to perform for the Jester Jack project. In that project a crank was used to generate a steady stream of events.  The engine naturally queued up those events, but the queue would grow so fast that there was a noticeable delay when the crank stopped. To overcome this the engines event queue was modified to only queue a few events.  The concept of hertz restricting the crank event generator would have solved this problem.

Conclusion
--------------
The goal was to write a robotic program structured in the Pico-Engine to control a simulated robot empowered exploration of the Pico engine and its ability to intergrade with ROS embedded systems.  The benefit of doing this would be ease of program design and development for large scale system similar to robots.  For example, such a system a young Will Robinson could modify to alert himself of danger.  This investigation shows the Pico engine has great potential for this application but needs to refine some technology for seamless integration with ROS. I was able to get Gazebo running in Mac OSX but had to start fresh in Linux for the lack of support for ROS in Mac OSX. I was further detoured with the lack of support for Linux in Virtualbox on Mac OSX hosts. I was able to get through a few ROS examples before trying to create a ROS control layer for Gazebo simulator, at which point my VirtualBox instance of Linux became unmanageable. I found these sources https://www.npmjs.com/package/ros-backbone , http://wiki.ros.org/rosnodejs which will serve as a good start for integrating Pico’s with ROS.  The Pico-Engine will be able to combine with ROS after resolving the issues listed above.  Overcoming the development environment questions may be the next step in continuing the goal of writing a robotic program structured in the Pico-engine. 
