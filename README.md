Refer to https://youtu.be/QfNvhPx5Px8 all the explaination is for this video.

**IF YOU ARE FACING ERRORS, READ THIS POST. IT ADDS TO THINGS TYPED BY SIRAJ IN THE VIDEO. OTHER THAN WINDOWS USERS MAY IGNORE JUST THE DOCKER AND IMAGE PATH PART. REST IS FOR ALL**

Okay so this comment is for benefit of beginners like me. From my personal experience I can say that, you would probably face lots of errors while executing this program. So for your convenience, here are probably all the step-wise errors which I faced and how I solved them. Since youtube does not accept long comments, I''ll post this in parts, in reply of 1st part.
As told by siraj in the later comments, you can find the entire tutorial on: 
https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/?utm_campaign=chrome_series_machinelearning_063016&utm_source=gdev&utm_medium=yt-desc&authuser=1#0

Just for information, I executed it on Windows

1) Installing Docker on Windows:
If you are running Windows 10 HOME or Windows 8.1 and below, you would need "docker toolbox". If you have Windows 10 pro/enterprise consider downloading "docker for windows". For knowing difference and further information visit - https://docs.docker.com/engine/installation/windows/
While Installing docker, I clicked the last checkbox of 'install Virtual Box' (something like this). You may or may not select this.﻿

2) Downloading Tensorflow image:
while typing the command, make sure you type "gcr.io/tensorflow/tensorflow:latest-devel". Because if you are referring to https://www.tensorflow.org/versions/r0.7/get_started/os_setup.html#download-and-setup for initial installation, they have mentioned "b.gcr.io/t...." however in the later part you will have to use "gcr.io/..." so its better not to use "b.gcr.io/..." because otherwise it throws error.
After typing and hitting enter, it will say 'image not found locally' don't panic wait for 2 seconds, it will download all the things. Once you see "#" on the left side, this indicates your download and installation is complete and you are currently in the TF image. Hit "ctrl+D" this brings you out of any image or python execution.

3) Making image directory:
you can use the commands shown by siraj. If you are using them remember to use "/" for path and not "\". Windows by default uses "\" for directory path, but since docker is bash environment, use "/". Here "\" is used as delimiter which you could use if your folder name includes two letters eg. "Darth\ Vader" this considers the space between Darth and Vader. And don't type full windows address like "C:\Users\..." the docker environment's HOME or ~ is by default in "C:\Users\<user_name>\" so type the directory path for further path. You could always manually create new folder at this location and copy/cut + paste image dataset in tf_files folder created here.

4) Downloading image dataset:
You "HAVE TO DOWNLOAD .JPG" type of images only. Because in the later part it won't accept other types. In my case, initially fatkun used to crash number of times for so many(500-700) images. So I tried many other ways. I used "Down them all" in firefox but it mostly downloads images in .jpe format which gave me an error later. But later when I again installed fatkun, by God's grace it worked well. While downloading make sure on the google images site you scroll down till the end where no images are further left to load and all the images are appearing on website. Now click fatkun icon -> "this tab" -> deselect irrelevant images like g+,twitter,fb icons -> more options (on top) -> click "rename based on" -> click save image. Make sure you download at least 2 types of images like Darth Vader and Darth Maul because this is multiclass classifier.

5)  Linking TF image to Dataset:
After typing command "docker run -it -v..." and hitting enter, for 1st time it would download the image. Then you would see "#" on left. Now, you have to type all the later commands beside this # only. 1st make sure you find your image folders by typing " ls /tf_files/star_wars/". If you get error like file not found or "python ....." file not found in this or later step,linking hasn't occurred properly. type ctrl+D, now besides $ again type command "docker run -it -v...." and proceed further. type "cd /tensorflow" because unless you type "/" it won't go into the directory.

6) Retrain model:
As mentioned earlier, the command "python tensorflow/example/..." is to be typed besides "#" which you see after linking TF image to dataset. after typing all those commands if you see some error like file not found etc. press ctrl+D and again start execution from the step of linking the TF image to dataset.
If you see error as "image not jpg...less than 0x80 0x90" (something like this) :
see the line above it, "creating bottleneck....<image_name>.txt". Go to that folder and delete that image.Come back to docker, now no need to type everything again. TF stores bottlenecks in cache.  just type 'up arrow key', you would see "python tensorflow/examples...." every command side by side. No worries, hit enter, it will start from where it has left.

7) Classify:
make sure after typing "import tensorflow as tf" in the next line you add "import sys". This would accept sys.adv[1].
On line 22 of code shown by siraj, make sure you hit enter after "..., \" and type the rest part in next line.
Remember the name by which you saved this python script.For ease of access, save it in folder "tf_files".
Now open a fresh docker window, type the linking command of "docker run -it -v $HOME/...." as mentioned in step 5. Then type the command "python /tf_files/<script_name_you_assigned>.py  .....<image_name>.jpg" here since siraj's script name is label_image, he has typed that name, you have to type the script name which you assigned. It will show some random lines and then ratio of the class in which this image falls.
eg. maul (score = 0.87596)
      darth vader (score = 0.12404)

CONGRATULATIONS!!! YOU HAVE SUCCESSFULLY BUILT YOUR FIRST IMAGE CLASSIFIER.
