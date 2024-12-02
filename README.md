# ros2_for_unity

ROS-TCP-Endpoint公式[こちら](https://github.com/Unity-Technologies/ROS-TCP-Connector?tab=readme-ov-file#installation)

ROS TCP Connectorをbuildやりかた。

レポジトリをcloneする際はｰbでブランチ指定します。

（2024年11月時点ではv0.7.0がインストールされます）

```
 mkdir -p ~/ros2_for_unity/src
 cd ~/ros2_for_unity/src
 git clone -b main-ros2 https://github.com/Unity-Technologies/ROS-TCP-Endpoint
 cd ..
 colcon build --symlink-install
 source ~/ros2_for_unity/install/setup.bash
```

### 使い方
AkariUnityのレポジトリは[こちら](https://github.com/mantues/akari_sim_unity/tree/master?tab=readme-ov-file)


#### ros_tcp_endpointを実行

ROS_IPではローカルホストを指定しています。

```
ros2 run ros_tcp_endpoint default_server_endpoint  -ros-args -p ROS_IP:=127.0.0.1
```

Unity側と通信が確立されていれば左上のROS2IPの矢印が青くなります。

![alt text](<./images/akari1.png>)

#### Subscriberの確認

通信が確立されていればUnity側からトピック[/simple_topic]が送られてきてるので確認できます。

別コンソールを立ち上げて下記コマンドで確認できます。

```
cd ~/ros2_for_unity
source install/setup.bash
ros2 topic echo /simple_topic
```

うまく行くと下記のようなデータが表示されます。
data: '6:29:43'


下記でも確認できます。

```
cd ~/ros2_for_unity
source install/setup.bash
ros2 run py_pubsub listener
```

うまく行くと下記のようなデータが表示されます。

[INFO] [1733175111.468872446] [minimal_subscriber]: I heard: "6:31:51"


#### Publisherの確認

別コンソールを立ち上げて下記コマンドでPublisherの確認ができます。

```
cd ~/ros2_for_unity
source install/setup.bash
ros2 run py_pubsub talker
```

うまく行くとUnity側のコンソールに受信したデータが表示されます

![alt text](<./images/akari2.png>)
