# Innovations in Kitchen Robotics: Dexterous Knife Manipulation

### Alex Rice, Gage Rodriguez, Yos Wagenmans

Dexterous manipulation continues to be a challenge for robotic controllers. Cutting objects, a task trivial to humans, requires significant overhead to allow a robot to execute without human input. Previous work has focused on various stages of cutting, from tool manipulation, to the dynamics of food as it is cut, to planning optimal knife trajectories. We seek to enable a system that can perceive a knife in its environment, grasp it in a manner that enables cutting, and then position the blade of the knife such that it can cut an object. Though this system has potential direct applications in automating kitchen tasks, we also see value in its addition to the foundation of our understanding of robotic tool manipulation, especially when said manipulation also affects other objects in the world.

## Development of Object Models and Simulation

To develop an informative simulation, we first set up an environment to model the relevant problem parameters. We set up our environment to resemble a simplified kitchen. It includes 3 table upon which the knife we will be manipulating, a knife holder, the object we are going to cut, and a Kuka Iiwa at rest. 

![](https://github.com/alexrice236/6.4210Final/blob/main/im/apple.JPG)

![](https://github.com/alexrice236/6.4210Final/blob/main/im/cleaver.JPG)

![](https://github.com/alexrice236/6.4210Final/blob/main/im/knifeholder.JPG)

## Generating Point Clouds

To progress towards grasping the knife, we first need to identify the location of the knife in the world frame. We approach this problem using iterative closest point (ICP). Using our environment setup, we construct the necessary foundation for ICP. We pull information from the RGBd sensor in our environment that is pointing at the knife, extracting a point cloud consisting of the knife, knife-holder, and some of the surrounding table. This is our source point cloud. Since the size and shape of the knife are not unknowns for this task, but rather the location of the knife is what we are interested in, we provide our simulation with a point cloud of solely the knife. Taking the .obj file of the knife, we are able to extract a mesh and construct a ”true” point cloud, referred to as the model point cloud. With this foundational information, we then move to processing the point cloud from our RGBd sensor, as it includes points that do not belong to the knife.

![](https://github.com/alexrice236/6.4210Final/blob/main/im/pc_w_table.JPG)

We focus on removing the points belonging to the table surface, as their planar nature makes them easier to identify. Fitting a plane to the points belonging to the table’s surface allows us to use RANSAC to remove them from our source point cloud.

![](https://github.com/alexrice236/6.4210Final/blob/main/im/pc_wo_table.JPG)

## Grasping the Knife

Achieving a grasp on the knife required a few additional steps after determining the pose of the knife. Since we use a ”two-fingered” gripper, the knife must be approached in such a way that there is no collision before a correct grip is made. As such, we added an additional pose slightly above the knife handle, so the grasp could be made perfectly every time.

![](https://github.com/alexrice236/6.4210Final/blob/main/im/knife%20in%20holder.JPG)

![](https://github.com/alexrice236/6.4210Final/blob/main/im/pregrasp.JPG)

![](https://github.com/alexrice236/6.4210Final/blob/main/im/grab.JPG)

## Planning Trajectories

Given a start and end pose for the Iiwa, there needed to be a set of intermediate poses along the trajectory that represented the different translational and rotational changes of the robot gripper. This allowed us to better control the smoothness of the robot’s trajectory when moving throughout space. To do so, we employed Spherical Linear Interpolation (SLERP), which takes in and outputs quaternions and gives a map, or in our case, a list of intermediate 3D rotations of the gripper.

## Exploring Cutting Dynamics

Using known reference poses for our models (e.g. blade to handle distance, cutting target center to surface distance), we can approach and make contact with a cutting target but have yet to explore the potential of alternative cutting trajectories.

![](https://github.com/alexrice236/6.4210Final/blob/main/im/chop1.JPG)

![](https://github.com/alexrice236/6.4210Final/blob/main/im/chop2.JPG) 

