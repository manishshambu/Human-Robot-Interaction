The complete dataset (~3GB) can be found [here](https://drive.google.com/open?id=1GiSWJAvtohRwrDfnMptAHxRO7LuRT2lX) (requires CUBoulder sign-in).

Original dataset (captured using [this Processing script](https://github.com/manishshambu/Non-Verbal-Expression-For-Robots/blob/master/data_capture.pde)) contains 'frames/', 'projSpaceCoords.json', 'realWorldCoords.json', and 'myrecording.wav.' I generate all the other files from my gesture_modeling.ipynb code.

* frames/ -- contains combined depth (with skeleton superimposed) and RGB images from original capture.

* myrecording.wav -- audio portion of original recording

* mono_myrecording.wav -- mono-channel version of audio because Google Cloud Speech API only takes in Mono. So does the prosody software. Working with Mono just makes life easier overall.

* realWorldCoords.json -- list of dictionaries. # elements in list = # frames captured. each dictionary entry contains 'joint name': '[x,y,z]'. Coordinates are in [Kinect camera frame](https://www.informatik.uni-augsburg.de/lehrstuehle/hcm/projects/tools/fubi/img/OpenNI_Coordinate_System_small.png). There's another key called 'time_ms' which stores the timestamp in milliseconds (relative to start of data capture) of when this frame was captured.

* projSpaceCoords.json -- unused, but stored just in case. mapping of kinect camera frames coordinates to some other frame.
relative_joint_positions.json -- doesn't contains 'time_ms' key. otherwise, same format as realWorldCoords.json, except coordinates are relative to torso (hence, all relative coordinate values for torso are 0). {eg: relative coordinate for leftHand = realWorldCoord for left hand - realWorldCoord for torso}

* chunks/ -- contains .wav files and associated prosody features, one-hot encoded emotion features, and emoji ids. original myrecording.wav is segmented by portions of silence. Prosody = 13 features ([see this readme](https://github.com/jcvasquezc/DisVoice/blob/master/prosody/README.md)). One hot encoded emotion = 5x64 features (I'm looking at the top 5 emojis). Emoji ids = 5x5 features (one hot encoding is derived from this, [see this readme for emoji labels](https://github.com/bfelbo/DeepMoji/blob/master/emoji_overview.png)) -- unused, but stored just in case.
