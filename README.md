# depth-camera_Kimjeongyeon

**Depth Camera 플러그인 생성**

먼저 Gazebo에서 사용할 depth camera를 선택합니다. 저는 Microsoft Kinect를 사용하였습니다. Gazebo 홈페이지에서 제공하는 Kinect sensor를 다운로드한 후, 압축을 해제합니다.
이후, kinect 폴더를 ```~/.gazebo/models```로 옮깁니다.

Kinect의 디렉토리에 있는 ```model.sdf``` 열어 ```</camera>``` 태그 바로 뒤에 다음과 같은 SDF markup을 추가합니다.

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
      
        
