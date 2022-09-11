## Face recognition with Unity3D



# Overview
This project is an application of AR and face tracking. It is an android app that runs on arcore-supported devices. It maps out the user's face and tracks it. There are a few filters added to this app that users can switch from. Users can record the video of an ongoing session with the button on the bottom. The stored session will be stored in local device storage and can be accessed through a gallery or file manager. <br/>
Link for the project : 

# Components used:
### Unity 
Unity3D is a powerful cross-platform 3D engine and a user-friendly development environment. Unity is used for making games, and 3D and AR/VR applications for mobile, desktop, the web, and consoles.

### ARFoundation 
AR Foundation allows you to work with augmented reality platforms in a multi-platform way within Unity. [link](https://docs.unity3d.com/Manual/AROverview.html) 

### ARCore 
The ARCore XR Plugin package enables ARCore support via Unity's multi-platform XR API. [link](https://docs.unity3d.com/Packages/com.unity.xr.arcore@3.1/manual/index.html)

### NateCorder  
NatCorder is a lightweight, easy-to-use, full-feature video recording API for iOS and Android in Unity3D. [link](https://blog.natml.ai/natcorder-unity-recording-made-easy-f0fdee0b5055)

# How does it work?

It uses the ARCore package from ARFoundation for face recognition and tracking. In a hierarchy, there is ARCamera, inside AR Session Origin, which uses a camera script. This camera with help of the script tracks the face in the ongoing session.

AR Session Origin, has three main components, Swapping Filters which will go on the face, an AR face manager which takes a prefab and manages faces, and a session origin which takes the camera.

In the hierarchy, after AR Session Origin, there is a canvas component in which there is a change face button and a record button. The change face button simply loops between filters that are applied to the face, change face button takes AR Session Origin in the button section of the changing face.

For recording NatCroder is being used, there is a ReCm in the hierarchy which takes ReCm script which is for the camera. this goes in the RecordButton in the canvas component. as seen in fig.4.

# Architecture and project files

![archi.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662798374209/d7cDsc910.png align="center")
<p style="text-align: center;">Fig.1 Architecture</p>

![AR.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662800965216/guQiOGXb8.png align="left")
Fig.2

![Pfiles.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662801232016/h1PMdOInPv.png align="left")
Fig.3

![hieCan.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662801500346/xwkKvwu9m.png align="left")
Fig.4

![changeface.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1662801631065/DaOtq4F-0.PNG align="left")
Fig.5

# Final conclusion and relevant links
Hence this is a very small AR project which recognizes the face and then maps out the face which helps in tracking it. then apply a filter stored in the project to face and toggle between filters with a button and then record the desired session with the record button.

### Video for reference: 
[Face Tracking Filters with AR Foundations in Unity Workshop](https://www.youtube.com/watch?v=5-kpTHO3MpA&t=1077s)
