# Innovations in Kitchen Robotics: Dexterous Knife Manipulation

### Alex Rice, Gage Rodriguez, Yos Wagenmans

Dexterous manipulation continues to be a challenge
for robotic controllers. Cutting objects, a task trivial to humans,
requires significant overhead to allow a robot to execute without
human input. Previous work has focused on various stages of
cutting, from tool manipulation, to the dynamics of food as it
is cut, to planning optimal knife trajectories. In this paper, we
propose a system that captures the low-level fundamentals behind
the combination of the aforementioned processes. That is, we seek
to enable a system that can perceive a knife in its environment,
grasp it in a manner that enables cutting, and then position the
blade of the knife such that it can cut an object. Though this
system has potential direct applications in automating kitchen
tasks, we also see value in its addition to the foundation of our
understanding of robotic tool manipulation, especially when said
manipulation also affects other objects in the world.

## Development of Object Models and Simulation

To develop an informative simulation, we first set up an
environment to model the relevant problem parameters. We
set up our environment to resemble a simplified kitchen. It
includes 3 table upon which the knife we will be manipulating,
a knife holder, the object we are going to cut, and a Kuka
Iiwa at rest. 

