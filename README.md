# depth-camera_Kimjeongyeon

**Depth Camera 플러그인 생성**

먼저 Gazebo에서 사용할 depth camera를 선택합니다. 저는 Microsoft Kinect를 사용하였지만 다른 camera의 경우에도 과정은 동일합니다.
Gazebo Tutorial에서 제공하는 Kinect sensor를 다운로드한 후, 압축을 해제합니다.
이후, kinect 폴더를 ```~/.gazebo/models```로 옮깁니다.

Kinect의 디렉토리에 있는 ```model.sdf``` 파일을 열어 ```</camera>``` 태그 바로 뒤에 다음과 같은 SDF markup을 추가하고 저장합니다.

![kinect1](https://user-images.githubusercontent.com/84000076/122526009-cbcd6d00-d054-11eb-894c-3ab5aa959195.png)

 ```
 <plugin name="camera_plugin" filename="libgazebo_ros_openni_kinect.so">
          <baseline>0.2</baseline>
          <alwaysOn>true</alwaysOn>
          <!-- Keep this zero, update_rate in the parent <sensor> tag
            will control the frame rate. -->
          <updateRate>0.0</updateRate>
          <cameraName>camera_ir</cameraName>
          <imageTopicName>/camera/color/image_raw</imageTopicName>
          <cameraInfoTopicName>/camera/color/camera_info</cameraInfoTopicName>
          <depthImageTopicName>/camera/depth/image_raw</depthImageTopicName>
          <depthImageCameraInfoTopicName>/camera/depth/camera_info</depthImageCameraInfoTopicName>
          <pointCloudTopicName>/camera/depth/points</pointCloudTopicName>
          <frameName>camera_link</frameName>
          <pointCloudCutoff>0.5</pointCloudCutoff>
          <pointCloudCutoffMax>3.0</pointCloudCutoffMax>
          <distortionK1>0</distortionK1>
          <distortionK2>0</distortionK2>
          <distortionK3>0</distortionK3>
          <distortionT1>0</distortionT1>
          <distortionT2>0</distortionT2>
          <CxPrime>0</CxPrime>
          <Cx>0</Cx>
          <Cy>0</Cy>
          <focalLength>0</focalLength>
          <hackBaseline>0</hackBaseline>
        </plugin>
  ```
  ![kinect2](https://user-images.githubusercontent.com/84000076/122526046-d7b92f00-d054-11eb-8796-629f2e28cbde.png)


**Gazebo 내 depth camera 설치**

ROS 지원이 활성화 된 상태에서 Gazebo를 실행합니다.

```roslaunch gazebo_ros empty_world.launch```

이후 Insert에서 "Kinect ROS" 모델을 추가하고 카메라 앞에 상자 2개를 추가하였습니다.

![kinect4](https://user-images.githubusercontent.com/84000076/122526670-8493ac00-d055-11eb-9bed-ad7bb430f282.png)

**RViz에서 depth camera 출력 보기**

먼저 RViz를 실행합니다.

```rosrun rviz rviz```

그 다음 Add에서 PointCloud2와 Image를 추가합니다. Image는 <imageTopicName>에서 사용한 값으로 설정해주고, PointCloud2는 <depthImageTopicName>에서 사용한 이름으로 설정해줍니다.
 
![kinect5](https://user-images.githubusercontent.com/84000076/122527634-75f9c480-d056-11eb-8495-c5c349fa7736.png)
![kinect6](https://user-images.githubusercontent.com/84000076/122527646-7a25e200-d056-11eb-80a4-2ec009858157.png)

이후, Rviz에서 일반적인 camera와 depth camera 두 가지 경우를 선택하여 출력을 볼 수 있습니다.

![kinect7](https://user-images.githubusercontent.com/84000076/122528062-e56fb400-d056-11eb-95a6-04fae3692e74.png)
![kinect8](https://user-images.githubusercontent.com/84000076/122528083-ea346800-d056-11eb-8a10-78dccd0675cd.png)
