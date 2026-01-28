项目功能模块：
（1） 车辆基础控制：
系统登录、系统主控界面、基本运动控制、安全控制保护
（2）实时状态监控：
状态数据采集、状态数据传输、状态数据显示、历史数据管理
（3）任务执行管理：
地图构建、定点巡逻、目标识别、目标跟踪、自主探索、智能避障、空地协同、人机协同
（4）传感数据管理：
传感数据采集、传感数据显示、传感数据传输、历史数据管理
（5）集群协同通信：
集群组队设置、队内单点通信、队内广播通信、通信监听控制
（6）设备配置管理：
设备信息设置、网络连接设置、机载组件参数、系统运行日志


项目文件结构
MICCProject1/
├── CMakeLists.txt
├── package.xml
├── setup.py
├── requirements.txt
├── README.md
│
├── launch/                           # ROS 启动文件
│   ├── ugv_base.launch
│   ├── ugv_state.launch
│   ├── ugv_task.launch
│   ├── ugv_sensor.launch
│   ├── ugv_comm.launch
│   ├── ugv_gui.launch
│   └── ugv_full.launch
│
├── config/                           # YAML 参数配置
│   ├── vehicle.yaml
│   ├── sensors.yaml
│   ├── network.yaml
│   ├── tasks.yaml
│   ├── ui.yaml
│   └── logging.yaml
│
├── scripts/                          # ROS 可执行节点（入口）
│   ├── base_control_node.py
│   ├── state_monitor_node.py
│   ├── task_manager_node.py
│   ├── sensor_manager_node.py
│   ├── cluster_comm_node.py
│   ├── device_config_node.py
│   └── gui_bridge_node.py           # GUI 与 ROS 的桥接节点
│
├── src/
│   └── ugv_edge_system/
│       ├── __init__.py
│
│       ├── common/                   # 通用工具层（无 ROS 依赖）
│       │   ├── __init__.py
│       │   ├── config_loader.py
│       │   ├── logger.py
│       │   ├── time_utils.py
│       │   ├── data_buffer.py
│       │   └── constants.py
│
│       ├── ros_interface/            # ROS 封装层（强 ROS 依赖）
│       │   ├── __init__.py
│       │   ├── topic_manager.py
│       │   ├── service_manager.py
│       │   ├── action_manager.py
│       │   └── ros_state_cache.py
│
│       ├── base_control/              # （1）车辆基础控制
│       │   ├── __init__.py
│       │   ├── motion_control.py
│       │   ├── safety_guard.py
│       │   ├── mode_manager.py
│       │   └── chassis_adapter.py
│
│       ├── state_monitor/             # （2）实时状态监控
│       │   ├── __init__.py
│       │   ├── state_collector.py
│       │   ├── state_processor.py
│       │   ├── state_publisher.py
│       │   └── history_manager.py
│
│       ├── task_management/           # （3）任务执行管理
│       │   ├── __init__.py
│       │   ├── task_manager.py
│       │   ├── task_scheduler.py
│       │   ├── task_executor.py
│       │   ├── map_builder.py
│       │   ├── patrol.py
│       │   ├── target_detection.py
│       │   ├── target_tracking.py
│       │   ├── exploration.py
│       │   ├── obstacle_avoidance.py
│       │   ├── air_ground_coop.py
│       │   └── human_machine_coop.py
│
│       ├── sensor_management/         # （4）传感数据管理
│       │   ├── __init__.py
│       │   ├── drivers/
│       │   │   ├── __init__.py
│       │   │   ├── lidar.py
│       │   │   ├── camera.py
│       │   │   ├── imu.py
│       │   │   └── ultrasonic.py
│       │   ├── sensor_collector.py
│       │   ├── sensor_processor.py
│       │   ├── sensor_publisher.py
│       │   └── history_manager.py
│
│       ├── cluster_communication/     # （5）集群协同通信
│       │   ├── __init__.py
│       │   ├── team_manager.py
│       │   ├── unicast.py
│       │   ├── broadcast.py
│       │   ├── listener.py
│       │   └── message_router.py
│
│       ├── device_config/             # （6）设备配置管理
│       │   ├── __init__.py
│       │   ├── device_info.py
│       │   ├── network_config.py
│       │   ├── component_config.py
│       │   ├── log_manager.py
│       │   └── diagnostics.py
│
│       └── gui/                       # ⭐ PyQt GUI 模块（重点）
│           ├── __init__.py
│           ├── app.py                 # PyQt 应用入口
│           │
│           ├── bridge/                # GUI ↔ ROS 通信
│           │   ├── __init__.py
│           │   ├── ros_subscriber.py
│           │   ├── ros_publisher.py
│           │   └── ros_service_client.py
│           │
│           ├── main_window.py         # 主窗口
│           │
│           ├── pages/                 # 各功能页面
│           │   ├── __init__.py
│           │   ├── login_page.py
│           │   ├── dashboard_page.py
│           │   ├── control_page.py
│           │   ├── state_monitor_page.py
│           │   ├── task_manager_page.py
│           │   ├── sensor_page.py
│           │   ├── cluster_page.py
│           │   └── config_page.py
│           │
│           ├── widgets/               # 可复用控件
│           │   ├── __init__.py
│           │   ├── status_card.py
│           │   ├── video_widget.py
│           │   ├── map_widget.py
│           │   └── log_viewer.py
│           │
│           ├── resources/             # UI 资源
│           │   ├── icons/
│           │   ├── images/
│           │   └── styles.qss
│           │
│           └── models/                # GUI 数据模型
│               ├── __init__.py
│               ├── vehicle_state_model.py
│               ├── task_state_model.py
│               └── sensor_state_model.py
│
├── msg/                              # ROS 消息
│   ├── VehicleState.msg
│   ├── TaskStatus.msg
│   ├── SensorStatus.msg
│   └── ClusterMessage.msg
│
├── srv/                              # ROS 服务
│   ├── StartTask.srv
│   ├── StopTask.srv
│   ├── EmergencyStop.srv
│
└── logs/
    └── ugv_runtime.log
