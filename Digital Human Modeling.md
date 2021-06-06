# Human Operator Modeling

**Author**: Pavel Popov

**Email**: [pavel.popov@mail.polimi.it](mailto:pavel.popov@mail.polimi.it)


# 1 Introduction

In this project my group was focused on Human Operator Modeling for industrial environments. This task required us several steps of research and practical application in 3D modeling and analysis. Below you will find the result with some explanations, split into several parts which we identified during the project.
Our task was to represent a human operator in a condition of working with the industrial machine, analyze his movements in the space and estimate danger or inefficiencies. The research has been started from a general workflow, heavily used in Computer Graphics, Game Development companies and studios. This pipeline includes some steps for a creation of visually equal model which includes inverse kinematics and can be managed and moved manually, using algorithms, or special systems. We refer to this approach as ‘Human Body Surface’ creation. Therefore, this approach assumes a precise model of a human body represented as a mesh, which, when gone through the process of rigging, can be managed, and moved as a real-human body. However, this approach does not consider specific constraints of a human body and is relied on an assumption of a user that works with a particular model. 
From the other side, we consider more precise (also more difficult) approach for more precise implementation of a human body into a digital world. This workflow includes some specific software used by experts of ergonomics and medicine. Using this pipeline, it is possible to create and analyze a human body as a system of muscles and joints working together.

# 2 Human body surface model

This section will focus on the first approach to create a human model. There are software and pipelines described.
Let us define general steps to create a model that can be represented in a digital environment:
1- Mesh modeling, here the main mesh of the human-like model is defined.
2- Scaling
3- Topology optimization
4- Rigging
5- Exporting

I will go through some of this steps using several software packages that is used in a real-world production.

## 2.1 Formats and Software

Considering this approach, we can rely on years of development inside the sphere of Computer Graphics and Game Development. Both these spheres were on a frontier of the modeling not only humans, but also complex environments where people live in. It is out of the scope of this report to review if CG used mesh modelling followed by rigging before Game Development. Anyway, this approach, at the moment, is the most widespread. Therefore, during many years of experience there were a lot of software developed for creation of digital people. Some of them are proprietary, but also there are several great open-source analogs on a stage today.
First, let’s describe what we want to see as a result of our pipeline. We expect to have visually and logically precise model of a human. It means that the model should look like a human, be a size of a human and textured as a human.
Based on the experience of CG world, we can identify that most widespread formats in which human models can be stored are following:

.obj - geometry definition file format first developed by Wavefront Technologies for its Advanced Visualizer animation package.
.fbx - proprietary file format (.fbx) developed by Kaydara and owned by Autodesk since 2006
.BVH - character animation file format was developed by Biovision, a defunct motion capture services company, to give motion capture data to customers. This format largely displaced an earlier format Biovision providing skeleton hierarchy information as well as motion data.
.dae - or Collada, is managed by the nonprofit technology consortium, the Khronos Group, and has been adopted by ISO as a publicly available specification, ISO/PAS 17506. COLLADA defines an open standard XML schema for exchanging digital assets among various graphics software applications that might otherwise store their assets in incompatible file formats. COLLADA documents that describe digital assets are XML files, usually identified with a .dae (digital asset exchange).

.glb/gltf – 3D data format used for representation of 3D scene in web environments. AVATAR project also focuses on the web representation using Babylon.js, so these formats I will consider separately.


# Software

All software that we will consider in this part is very known not only among specialists in CG but also to many people that used to do any 3D modelling on a computer. Let us mention several software on a stage.
At first, it is necessary to mention Blender. It is open-source package that can be used for literally all the steps needed to create a model. 
However, the pipeline is usually spit between different software. The reason is that some of them are better for a particular step in a workflow. Of course, moving between software is a problem (it can be problem of scale, formats and other) but in a CG studio the workflow is usually a trade-off between using several programs. Let us consider some of them for each step of human modeling. This list if based on the assumptions of the author.

1- Mesh Creation. Here the leaders are ZBrush (allows to create meshes in a sculpting mode and highly tuned for it), Blender and MakeHuman
2- Texturing. Blender, MakeHuman
3- Scaling. Blender 
4- Rigging. Blender, MakeHuman

Most of the formats and software, as it is usually in the modern world, were created by companies to solve a particular issue. Then these formats and (sometimes) software became open-source and de-facto (sometimes de-jure) standard for the sphere.

I will consider approach which is so far the best according to the speed, precision and usability for full creation of a human model.

## 2.2 Creation of a generic body surface model

There are several ways to start creating a model. Starting from manual mesh sculpting, where the user is free to create any shape or detail of a human body to more general approaches using pre-defined forms and shapes.
The AVATAR case is not focusing on visually highly-detailed models. So, the approach was used cover a low-precision model. 
For this case, the best software defined is MakeHuman. 
This software allows to go through all the process of model creation.
Starting from a base template, user is free to change a big number of parameters using sliders. After that, there are several types of texturing available. However, you can texture the model itself after exporting it using all major formats. Also, this software provides automatic rigging and there are several topologies to use. Rigging in CG is a process of combining skeleton model and a mesh in a way that it behaves as a complete system.
One of the main features of MakeHuman is a set of 4 rigging options. They vary by different number of ‘bones’ applied to the human-like mesh. This can be useful when creating models for different reasons. For example, sometimes, only general movements but for many units need to be simulated in a digital world. In this case it is better to simplify bones system and apply as many joints as possible for accurate representation of each human model. From the other side, sometimes more complex behavior is required for a model e.g facial expressions or finger movements. MakeHuman allows to create a maximum number of 163 bones.

The final model created in a program can be exported in many formats.

![Formats Available](https://raw.githubusercontent.com/FTi130/Avatar-DigitalHumanModeling/main/00%20Toolkit/01%20Body%20Surface%20Model/Formats.png)

## 2.3 Scaling and Rigging

However, sometimes there are changes needed for a generated model. In this case all changes can be made directly in 3D modelling software. I was using Blender and Rhinoceros during AVATAR project. Rhinoceros part will be mentioned later in this report. 
There are many ways the model can be loaded in Blender. Many formats can be used, but sometimes problems of scale or orientation appear. For me it was easier to fix all issues manually in Blender but there are several plugins that can help to work with the model normalization.

Export from MakeHuman to Blender is not straightforward but pretty easy. After defining the model, we already can have pretty all the bones and meshes out from the box.
Also, Make Human allows to create initiate Pose for your model. You can also check if there is enough precision in the rigging system you have choosen.

![Rendered Pose](https://raw.githubusercontent.com/FTi130/Avatar-DigitalHumanModeling/main/02%20Pictures/RenderPose2.png)
![Rigged Pose](https://raw.githubusercontent.com/FTi130/Avatar-DigitalHumanModeling/main/02%20Pictures/Rig2.png)

You can find some example stored as .fbx, .dae and .obj files in the folder 01. I used two different approaches to create a model of a male and female. Also, two models differ from each other by number of joints and by topologies. Based on the personal experience, the best format is .fbx. It creates less problems when exporting and importing between programs, also it allows to store all the data in a single file when .obj format needs to be supported by .mtl file storing materials data.

I consider .glb/.gltf formats separately, because this is not a standart data transfer format for CG and modeling. Glb format was created to optimize the usage of 3D models in Web environments. Last years, web 3D was developing fast and popular engines were created to create static and dynamic 3D scenes. The leaders so far are Three.js and Babylon.js. These engines (I also call it libraries below) have many possibilities and able to work directly with .obj files. However,  .glb format is optimized for working with WebGL environments. The difference between glb and gltf is in the view of the data inside. When .glb format store the data in a binary code, .gltf is using JSON representation. JSON allows to store the data in a human-readable format that can be fit into existing databases. From the other side, files stored in .glb require less space on a disk.

You can find reliable explanations of working with .glb files on the website of [Khronos Group](https://www.khronos.org/blog/art-pipeline-for-gltf).



# 3 Human musculoskeletal model. [Tao Zhu](https://github.com/Antoni950425) part

This section will briefly explain how to use Opensim for mulsculoskeletal scaling and Inverse Kinematics. At the end of this part you should have a musculoskeletal model based on anthropometric data and an Opensim motion file based on Kinect raw data. These files can provide a good basis for later biomechanic analysis.

## 3.1 Softwares and model format

Opensim was chosen for modeling the human musculoskeletal system. OpenSim is a opensource software that allows a wide range of studies in the neuromusculoskeletal system, including analysis of walking dynamics, studies of sports performance, simulations of surgical procedures, analysis of joint loads, design of medical devices, and animation of human and animal movement. It provided a shared platform for accessing the musculoskeletal system. There are many existing models available in the repository ready for use. An Opensim model made from different components can be different according to the different purposes of the simulation, for instance, for simulating human walking, the joint mainly specifies the articulations at the pelvis, hip, knee, and ankle joints, etc.

An OpenSim model typically in .OSIM suffix can be used to represent body structures such as bodies, joints, and muscles. Thanks to the graphical interface, the human body can be easily modeled in detail through it, if you have knowledge of anatomy and biomechanics.

## 3.2 Selected generic musculoskeletal model

As modeling human musculoskeletal models require a lot of knowledge of anatomy, I did not choose to model by myself but rather chose open-source models that are already in the Opensim repository. The chosen models focus on the whole body, not in particular body segments, and here I found two models which are available. The first one was provided by Andrea Menegolo. [https://simtk.org/projects/ulb_project](https://simtk.org/projects/ulb_project). The second one was provided by Apoorva Rajagopal. [https://simtk.org/projects/full_body](https://simtk.org/projects/full_body) The examples in this document were carried out using models provided by Apoorva Rajagopal.

## 3.3 Change body proportion of the musculoskeletal model

In Opensim, the process of modifies the anthropometric data of a model is called scaling, Scaling is typically performed by comparing experimental marker data to virtual markers placed on a model, In OpenSim, the scaling step adjusts both the mass properties, as well as the dimensions of the body segments.

In order to run a scaling process, three input is required: The first is a Generic model provided by Opensim, depends on the different research purposes, the musculoskeletal structures can vary from each model, the picture here shows a model designed for gait analysis, so we can see it more focused on lower limb part. The second input file is the Marker files in trc suffix, it is usually several seconds of data with the subject posed in a static position. The last file required for scaling is the setup file for the Scale Tool, a file to teach Opensim how to compare the virtual markers to match experimental marker locations captured from the subject. With these three files, the anthropometry of the generic model will match the anthropometry of the particular subject.


About the three inputs of the scaling process: a generic model, a marker file, and a scale setup file. As mentioned, to obtain a marker file, the usual method is to use a motion capture device to capture the virtual markers placed in a real human. So we will face some difficulties to get a marker file from 1D anthropometry data. Therefore knowing how the scaling process works are very important for figuring out a way to generate a marker file from 1D anthropometry data. When performing the scaling process, Opensim will try to get the coordinates of each marker in real life and then compare these markers with the virtual markers on the virtual human model. Assuming that there are A1 and A2 markers in real space and B1 and B2 markers in virtual space, Opensim will calculate the distance M1 from A1 to A2 and the distance E1 between B1 and B2 and divide E1 and M1 to obtain the scale factor S1. If A1 and A2 are placed on the right leg bone, for example in the picture A1=R.ASIS, A2=R.Knee. Lat. Opensim will then scale the corresponding leg bone according to the scale factor S1. If the marker of the left leg bone is also captured, the corresponding left leg bone will also have a scale factor S2.

There are three requirements for placing the markers: 1. at least place three markers to track the position and orientation of a particular body segment. 2. better to place markers in anatomical locations with the least skin and muscle movement. 3. reference markers set provided by Opensim can be used. For the scaling process, requirements 1 and 3 are not important for now, the second requirement is crucial for adopting the 1D anthropometric data in the scaling process.

Where are the anatomical locations of the human body? Or in another term bony landmarks. The bony landmark is any place on the skin surface where the underlying bone is normally close to the surface and easily palpable. The picture below illustrates the bony landmarks of the human body.


For OpenSim, the bony landmarks are the most reliable markers for the scaling process. However, in many studies where anthropometric data were collected, most of the data collected did not contain a definition of bony landmark, so we needed to review the definitions in detail and filter out the data that contained bony landmarks to help Opensim perform scaling operations. In this document, I used the dutch adults’ data from Dined as an example to show the filtering process.


As you can see from the picture above, the selected bony landmarks were marked out in green. They are Vertex from Stature, Acromion from Shoulder Height, Elbow from elbow height, Trochanter from hip height, Fingertip from the elbow-fingertip length, Knee height from popliteal height sitting. These markers can give a basic scale of the upper limb and lower limb. As anthropometric data is not originally collected to provide detailed data for anatomy, we are missing many details such as ankles, the width of the body segments, etc. But for ergonomics analysis, these data can provide a basis for anthropometric scaling in Opensim.

## 3.4 Workflow of the scaling process

As anthropometric scaling in Opensim is a tedious process, not only about creating marker files but also needs to set up the correct virtual markers to be placed on the virtual human model, as well as the scaling configuration files. These files make the scaling operations incredibly cumbersome for the average user, so a simple toolkit has been created that allows users to quickly perform scaling operations when using the Dined anthropometric database. However, there are limitations to this toolkit; if some data is missing/not found from the anthropometric database, or if the data is defined differently, then the scaling process will not work and need to be redesigned from the beginning.

## 3.5 Change posture and movement of the musculoskeletal model

In Opensim, the function for creating human movements is called Inverse Kinematics (IK). This tool uses experimental data from each time period to create coherent human movements by positioning the model in the pose that 'best matches' the experimental Marker and coordinating data for that time period. The final output of the IK process is an MOT file, meaning motion files, the motion can be used for another OpenSim model, with the same marker set. Opensim's IK tool will use a set of algorithms to obtain the pose with the least error, and we need to assign different weights to the Marker in Opensim's IK configuration files to help Opensim to perform the calculations. In general, to perform an IK activity we need the following inputs: a generic full-body musculoskeletal model of the human. A marker file with a .trc suffix, which is usually a set of markers obtained from a motion capture system (sample like the file in the scaling process). Finally, the configuration file which weights each marker. With these three files, we can perform Inverse Kinematics operations on the generic musculoskeletal model in Opensim.

But since Kinect is a markerless motion capture system, we do not have access to the coordinates of the real Marker in the human body, and it seems that we cannot perform Inverse Kinematics operations. However, this problem can be solved by reviewing the raw Kinect data and it is not hard to see that the raw data defines the change in position of each joint in space. In the diagram below, there are 25 body joints defined. So if we look at these joints as real markers which are placed on the body, we can perform IK activities through Opensim. (which means place OpenSim markers inside the musculoskeletal model) As can be expected, this approach is not 100% anatomically correct, but it can provide us with basic human movement data. In addition, our scaling model is derived from anthropometric data, so that the accuracy of scaling process of the human body during the IK activity is not very important to us.

However, the position of the Kinect joints cannot be used directly in Opensim, because the coordinate system of Kinect is different from Opensim. For example, the Kinect coordinates are centered on the Kinect camera, whereas the Opensim coordinates can be located in the center of both sides hips as the origin X and the YZ value of the Ankle on either side as the origin YZ value. In addition, we need to rotate the Kinect coordinate system by -90 degrees along the Y-axis to be the same as Opensim. Finally, the Kinect coordinate system has different units and you will need to calibrate it to get the units in real space, as Inverse Kinematics does not have very strong requirements for the dimension of the model (more about joints’ rotation), here you can simply multiply all the coordinates by 1000. you can visit these two links for more information:


## 3.6 Workflow of the inverse kinematic process in Opensim

The diagram above shows a basic Inverse Kinematic process, divided into three main steps, the first step is to acquire the Kinect raw data, the second step is to export the Kinect raw data to an Opensim Marker (.trc) file. The final step is to perform IK operations in Opensim.

In the first step, we will use a software called "LSL-KinectV2", which is an open-source motion capture software that can store Kinect data in a CSV file. If there is other software that can export Kinect raw data, feel free to use it.

In the second step, we need to use the excel tool provided to convert the acquired Kinect raw data into a marker file that Opensim can recognize. The main purpose of the excel tool is to convert the coordinate system of the Kinect data, and make an output that Opensim can recognize.

Finally, once we have the converted Kinect data in the .trc file, we can perform an inverse kinematic operation; the IK operation can generate a Motion file (.mot) which can be loaded into any size musculoskeletal model for biomechanical analysis. However, it is important to note that in order to make the IK results more accurate, we need to perform another scaling operation based on the Kinect data before the IK operation. First, load the generic human model and then turn on the scaling function. Load the IKScale.xml file, modify the mass data and click on the “run” button. After getting the scaled model, we can select the scaled model and turn on the inverse kinematic function, then load the IKConfiguration.xml file. Click on Run, then Opensim will start the IK operation. When the IK process is over you will find a motion file in the file path you assigned before. Before proceeding to the next step about analysis, first, the model previously scaled according to anthropometric data needs to be loaded and then the motion file needs to be loaded onto the scaled model too.


# 4 Motion tracking

## 4.1 Intro
It was coordinated with my colleagues that in this report I will provide only several approaches. Feel free to access other information in reports of my colleagues.I will describe Kinect SDK and Computer Vision workflows for capturing human movements.
Motion capturing, as well as model creation, is a well-known process for all spheres I mentioned above, such as CG or GameDev. There are many approaches and these years some more appear. I leave a system of marker based tracking and other special pipelines used in a high-ranking digital production.

Focusing first on Kinect approach. Kinect (also known as Project Natal) was created by Microsoft and is a motion-sensing device that uses depth-sensing camera to understand a scene in front of it. There is a proprietary software embedded by Microsoft and they continuously develop this project also for their Hololens system. However, there is an open SDK that can be used for creating custom extensions. One of this developments I mentioned while working on one architectural project which included kinetic rooftop and responsive facades. The work of [Hojoong Chung](https://github.com/hodgoong/grasshopper-kinect2) allowed me to represent myself directly in Rhinoceros viewport.https://github.com/hodgoong/grasshopper-kinect2

[Here](https://www.youtube.com/watch?v=f3-3cMmveTI) you can see an example of the result. This way of tracking is not the best in terms of precision. You can see in a video that some parts of the body are difficult to track, also the view angle of Kinect restricts motions of a person.


Last year company ARPM Design and Research presented different approach that involves Xbox and several ML algorithms. You can find it [food4rhino.com/en/app/catwalk/](here).





# 5 Custom Approach
## 5.1 The Idea
Previous part discussed creation of musculoskeletal model. It included usage of OpenSim – specific software package used for ergonomic analysis. However, the representation of muscles and joints of a human body represented as parametric geometries. This fact suggested me to look to what I am doing in the sphere of architecture and design. Namely, it seems to be possible to use parametric modeling and its software to represent models of a human in a similar logic as OpenSim does it but using only 3D software and Python. This part is a theoretical proposal. 
The software I choose are Rhinoceros and Grasshopper.
In previous part I described a process of motion capturing using Kinect SDK and real-time representation in Rhinoceros using Grasshopper. As you could see on the video, the body is represented as simple geometries – lines and spheres. Initially, I changed lines representation to a tube representation for my legs and arms. Using instruments of Grasshopper, I am able to work with this geometries in a way I need based on a simple structure provided by Kinect. This make me think of combining this approach with instruments used for tension and structure analysis in architecture. Such plugins as [Kangaroo](https://www.food4rhino.com/en/app/kangaroo-physics) or [Karamba](https://www.food4rhino.com/en/app/karamba3d) can be used to represent and analyze geometries as joints and muscles the same way it is done in OpenSim.
So far, without Kinect itself it is difficult to create a prototype of this system, therefore, it is only a theoretical proposal. As future works it can be developed as a plugin for Grasshopper that could be place on [the official plugin source](https://www.food4rhino.com/en)

# Conclusion

During the project I considered several approaches for a realistic human body modeling.  First of all, I described already existing and widespread apprach that involves standard software and formats for any CGI production. Secondly, me and my collegues considered a sophisticated approach using a special ergonomic analysis software. At the end, after workung on a second case, I realized that the same functionality can be achieved working only in a 3D design programs. However, Rhinoceros is the best 3D program at the market for many workflows, it is not very known out of the field of architecture and design. So, I could only theoretically describe a system allowing to
 have the functionality for ergonomic analysis using 3D software extensions. This work can be continued.
