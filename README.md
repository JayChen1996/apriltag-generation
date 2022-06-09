AprilTag-Generation
AprilTag-生成
===================

Generate AprilTags in custom layouts for [AprilTag 3](https://github.com/AprilRobotics/apriltag-generation).
为[AprilTag 3](https://github.com/AprilRobotics/apriltag-generation)生成自定义布局的AprilTag

# How to use the package
# 如何使用这个包

First, you will need to generate the code associated with the layout of your marker : 
首先，你需要生成与你的markgr布局相关的代码


~~~
ant
java -cp april.jar april.tag.TagFamilyGenerator <layout> <minimalHammingDistance>
~~~
The choices of layout are : 
layout的选择有：
- standard_x, new-style april tag with one pixel of data on the outside
- standard_x，新风格的april tag，有一个像素的数据在外部
- classic_x, old-style april tag
- classic_x, 旧风格的april tag
- circle_x, for circular april tag 
- circel_x，圆形的april tag
- custom_[...]. For more details about this last one, please check https://github.com/AprilRobotics/apriltag-generation/blob/master/src/april/tag/TagFamilyGenerator.java
- custom_[...]，更多信息请参见https://github.com/AprilRobotics/apriltag-generation/blob/master/src/april/tag/TagFamilyGenerator.java

With x the size of the tag (in pixels). The smaller is x, the faster the generation is.
x是tag(像素单位)的尺寸大小，x越小，生成的速度越快。

You will have as output into the terminal a string, starting from "package april.tag;" and ending at the end of the terminal.
This string is your new code that will be use for generating your markers. Save it into a .java file (ex : TagStandard20h9.java), into src/april/tag.


Then, execute : 

~~~ 
ant
~~~

Next, you can use this command to generate the C code associated with the marker : 

~~~
java -cp april.jar april.tag.TagToC april.tag.<name_of_new_java_file>
~~~

Or generate your new markers as .png : 

~~~
java -cp april.jar april.tag.GenerateTags april.tag.<name_of_new_java_file> .
~~~

NB : If the format of the markers is very small (ex : by default, 9x9 pixels), you'll need to rescale them. To do so, you may use the following command (Unix) : 

~~~
convert <small_marker>.png -scale <scale_chosen_in_percent>% <big_marker>.png
~~~

# Example usage for generating the 21h7 circular tag family:


```
$ ant
$ java -cp april.jar april.tag.TagFamilyGenerator circle_9 7
```
Then to generate the c code and tag images after copying the output into the source folder:
```
$ ant
$ java -cp april.jar april.tag.TagToC april.tag.TagCircle21h7
$ java -cp april.jar april.tag.GenerateTags april.tag.TagCircle21h7 .
```
