# rja_hololens
Joint Attention Training in Hololens
RJA Hololens Application
User : Person who is wearing Hololens
In this application 
We are using core components of Hololens-2 Hand Detection, Object Manipulator and Eye tracking to achieve our objective.
Hand detection and Object manipulator to interact with Avatar or to manipulate the transform component of Avatar.
Eye -Tracking to track the movement of eyes of the user.
https://learn.microsoft.com/en-us/windows/mixed-reality/design/eye-tracking
https://learn.microsoft.com/en-us/windows/mixed-reality/mrtk-unity/mrtk2/features/input/eye-tracking/eye-tracking-main?view=mrtkunity-2022-05

The application will first ask the user to look at the floor in order to detect the floor.
I used this article to achieve plane detection.
https://localjoost.github.io/Finding-the-Floor-with-HoloLens-2-and-MRTK-273/
After detecting plane, the application will prompt the user to identify whether the detected plane is a floor or not.
After detecting plane, a pop-up notification will be shown to user asking that whether the detected plane is a floor or not.
Now user can give the voice input saying “YES” if it is a plane or user can also click a button to give the feedback that this is a plane.
After taking the input from user app proceeds further.
An avatar will be spawned if the detected plane is a floor.
We can manipulate the position, rotation and scaling of the Avatar based on the requirements.
To manipulate the scaling of Avatar simply pinch the Avatar using both hands and stretch it to scale up and scale down. 
To move the Avatar on the plane just pinch it using only one hand then place it wherever you want.
To rotate the Avatar pinch it using both hands then rotate it whatever direction you want.
After we are done with the manipulation of Avatar, we can start the trial by clicking on the button.
To click the button simply move towards the button and click with finger just like a real button.
This button will tell the application that now user is ready for the trial.
We are using Eye-Tracking feature of Hololens 2. This feature enables the Hololens to track the eye movement of the user. It throws ray in the direction in which the user is looking and if the ray collides with any of the gameobject(which has collider on it) it gives the feedback to the application and based on this we can identify which object the user is looking at.
We can then check the object at which the user is looking at is this the targeted one or not and based on this we can give feedback to the user if he/she looked at the correct object or not.

We are using certain scripts to get the Input from the user and after receiving input process it to perform required actions.
“Target” script which is used to perform actions when the user looks at them. This script is attached to only those objects which are going to be our target which means only those objects which are supposed to be seen by the user or objects which are supposed to be hit by the ray thrown by the camera. This script also controls the rig movement of left and right hands of Avatar.
“PushButtonFollow” script helps the PushButton to follow the Target Gameobject (which is avatar in our case). This script initially calculates the offset value from the target then follows the target object.
“TargetManager” script determines the random target object then waits for the user to gaze at the Face of Avatar (at least for 3 seconds). After the user looks at the Face of Avatar event is triggered, and rig controller setup starts.
“AvatarRigController” script helps to control the rig movement of head of Avatar. It also restarts the trial once the user is done with the current trial.
“CharacterFaceManagement” script changes the default profile to Eye Tracking Profile and it disables the interaction with the Avatar so that the position and orientation of Avatar is going to remain fixed during whole session.
“HeadCollider” script notifies the user if he/she has stared at the target object for 3 seconds. To notify the user it shows a text “Start”.
