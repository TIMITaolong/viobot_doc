# Viobot数据包录制

Viobot里面是一个完整的ubuntu系统，无论是20.04还是22.04都支持完整的ROS的功能，所以可以通过ROS来录制数据包，用于现象记录或者是算法的参数调节。

需要注意的是，数据包可能会很大，设备自身的存储空间有限，需要外接高速内存卡。内存卡的写入速度至少在25M/S以上。

1.用于记录运行过程和现象

这个我们只需要录制开启了stereo2算法后的输出就可以了。

主要需要的话题就是`/zc_stereo2/warped_img`和 `/pr_loop/odometry_rect`，这两个话题分别是算法运行过程中提取了特征点并将双目图像合成后的图，可以看到算法在运行过程中的提点表现，其实也是对应上位机视频流输出的视频；另外一个话题是算法运行过程中设备相对于它初始位置的位姿变化，即设备运行过程的位姿，对应上位机上面的相机框的运动。

录包命令：

```bash
rosbag record /zc_stereo2/warped_img /pr_loop/odometry_rect -o /mnt/tfcard/run_record.bag
```

其中/mnt/sd\_card/run\_record.bag是所存的数据包的路径+名字，如果不在前面加路径就会录在你当前终端所在的路径，-o会自动给你所取名字增加一个时间在前面，方便区分不同时候录的包。

2.录制运行过程的原始传感器数据

录制了原始的传感器数据，可以通过SDK的for\_bag标志可以关掉设备原本的传感器数据读取，从而将数据包的数据作为算法的输入源来运行算法，可以用于算法的调参。

主要的话题包括`/image_left `、`/image_right` 、`/camera_left_info` 、`/camera_right_info`、`/imu`  如果是TOF版本需要开启TOF的话可以加一个话题`/tof_cloud`

录包命令：

```bash
rosbag record /image_left /image_right /camera_left_info /camera_right_info /imu -o /mnt/tfcard/raw_record.bag
```

其中/mnt/sd\_card/raw\_record.bag是所存的数据包的路径+名字，如果不在前面加路径就会录在你当前终端所在的路径，-o会自动给你所取名字增加一个时间在前面，方便区分不同时候录的包。
