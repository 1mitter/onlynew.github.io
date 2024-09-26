# Using IK with Virtual Skeleton

This asset supports [Final IK](https://assetstore.unity.com/packages/tools/animation/final-ik-14290?aid=1101lqGVS) by default. if you are using other IK, you will need to [modify script execution order](https://docs.unity3d.com/2021.3/Documentation/Manual/class-MonoManager.html). At the end of this chapter, you'll find configuration examples for several popular IK methods, such as [Final IK](https://assetstore.unity.com/packages/tools/animation/final-ik-14290?aid=1101lqGVS), [Bio IK](https://assetstore.unity.com/packages/tools/animation/bio-ik-67819?aid=1101lqGVS), [Unity 2D IK](https://docs.unity3d.com/Packages/com.unity.2d.animation@10.0/manual/2DIK.html) and [Unity Animation Rigging](https://docs.unity3d.com/Packages/com.unity.animation.rigging@latest). **Even if the IK you are using is not listed, you can still make it work by applying the underlying theory.**  

## Theory

Since most IK systems are designed for coupled skeletons, they cannot function correctly on decoupled skeletons. To ensure these IK scripts work properly, we need to create a familiar environment for them. We will generate a coupled virtual skeleton, similar to the one you typically use. 
Before the IK update, we will read the position and rotation data from the real skeleton and transfer it to the virtual skeleton. The IK script will then solve it on the virtual skeleton. After the IK update, the position and rotation data from the virtual skeleton will be written back to the real skeleton. To implement this process, we need to [modify script execution order](https://docs.unity3d.com/2021.3/Documentation/Manual/class-MonoManager.html).

![BP](/assets/img/Configuration/ScriptExecutionOrder.png)

Both Scalable Bone and IK work properly when the execution order of the scripts matches the flow shown below.

![BP](/assets/img/Configuration/normalOrder.png)

If your IK scripts are not solved in LateUpdate(), or if you are unable to modify the execution order of the IK scripts, then we need to follow another script execution order. In this order, IK scripts will override the animation and cannot interpolate between the solving result and the animation.

![BP](/assets/img/Configuration/override.png)
If you don't mind the IK calculations lagging by one frame, we can use a third method. Its advantage over the second method is that you can dynamically change the body proportions during runtime. 

![BP](/assets/img/Configuration/unknownOrder.png)

## Configuration Steps 
**Before you begin, please familiarize yourself with the standard usage of your IK to avoid misidentifying the source of errors**. 
Before proceeding, please setup Scalable Bone and create a virtual skeleton. 
### [Final IK](https://assetstore.unity.com/packages/tools/animation/final-ik-14290?aid=1101lqGVS)
1. Install your IK onto the virtual skeleton.
2. As this asset's script default execution order is compatible with Final IK, no modifications are required.

![BP](/assets/img/Configuration/FinalIK2.png)

3.Set "Fixed Transform" to false on Final IK inspector.
 
![BP](/assets/img/Configuration/FinalIK.png)

### [Bio IK](https://assetstore.unity.com/packages/tools/animation/bio-ik-67819?aid=1101lqGVS)
1. Install your IK onto the virtual skeleton.
2. Modify the script execution order as shown in the following picture.
 
![BP](/assets/img/Configuration/BioIK.png)

### [Unity 2D IK](https://docs.unity3d.com/Packages/com.unity.2d.animation@10.0/manual/2DIK.html)
1. Install your IK onto the virtual skeleton.
2. Modify the script execution order as shown in the following picture.
 
![BP](/assets/img/Configuration/Unity2DIK.png)

### [Unity Animation Rigging](https://docs.unity3d.com/Packages/com.unity.animation.rigging@latest)
1. Install your IK onto the virtual skeleton.
2. Modify the script execution order as shown in the following picture.
 
![BP](/assets/img/Configuration/AnimationRigging.png)

3.In the inspector of ReadTransform, clear the bonePair and add the bones covered by IK. In the inpector of WriteTransform, Set "SyncBonePair" to true.

![BP](/assets/img/Configuration/AnimationRigging2.png)

# See [gif demo](https://www.onlynew.tech/BodyProportions)
# Click [here](https://assetstore.unity.com/packages/slug/266535?aid=1101lqGVS) to purchase the assets.
 

