# 🎥 Web版智能摄像头监控系统

基于Flask + VLM的实时摄像头Web监控和AI分析系统

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-orange.svg)](https://opencv.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-red.svg)](https://pytorch.org/)

## ✨ 主要功能

- 🌐 **Web界面访问** - 通过浏览器实时查看摄像头画面
- 🤖 **VLM智能分析** - 使用Qwen2-VL-7B-Instruct模型进行视觉理解
- 📺 **实时视频流** - 支持RTSP网络摄像头和本地摄像头
- 📊 **实时监控面板** - 显示FPS、帧数、分析次数等统计信息
- 🔄 **定期AI分析** - 每10秒自动进行智能场景分析
- 📱 **响应式界面** - 支持桌面和移动设备访问
- 🎯 **RESTful API** - 提供状态查询API接口

## 🚀 快速开始

### 环境要求

- Python 3.8+
- CUDA支持的GPU (推荐，可选)
- 至少8GB内存
- 网络摄像头或RTSP摄像头

### 安装依赖

```bash
# 克隆项目
git clone https://github.com/yourusername/webcam-ai-monitor.git
cd webcam-ai-monitor

# 安装Python依赖
pip install -r requirements.txt

# 安装Qwen VL工具包
pip install qwen-vl-utils
```

### 运行系统

```bash
# 启动Web应用
python app.py
```

然后在浏览器中访问: **http://localhost:5000**

## ⚙️ 配置说明

### 摄像头配置

编辑 `app.py` 文件第24行，修改摄像头URL：

```python
# RTSP网络摄像头
self.camera_url = "rtsp://192.168.31.146:8554/unicast"

# 或使用本地摄像头
self.camera_url = 0  # 第一个摄像头
self.camera_url = 1  # 第二个摄像头
```

### AI分析配置

可以调整以下参数：

```python
# 分析间隔 (秒)
self.analysis_interval = 10.0

# 显示缩放比例
scale = 0.7  # 在get_frame_as_jpeg函数中

# JPEG质量
[cv2.IMWRITE_JPEG_QUALITY, 85]  # 在get_frame_as_jpeg函数中
```

## 📁 项目结构

```
webcam-ai-monitor/
├── app.py                 # 主应用程序
├── requirements.txt       # Python依赖列表
├── README.md              # 项目说明文档
├── .gitignore            # Git忽略文件
├── config.py             # 配置文件 (可选)
├── static/               # 静态资源目录 (可选)
└── templates/            # HTML模板目录 (可选)
```

## 🎯 系统架构

### 核心组件

1. **Flask Web服务器** - 提供HTTP服务和Web界面
2. **视频捕获线程** - 实时获取摄像头数据
3. **VLM分析线程** - 定期进行AI视觉分析
4. **视频流生成器** - 生成MJPEG视频流
5. **API接口** - 提供状态和分析结果API

### 工作流程

```
摄像头 → 视频捕获 → 帧缓存 → Web流媒体
                ↓
            VLM分析 → 结果缓存 → API输出
```

## 🌐 Web界面功能

### 主界面
- 实时视频流显示
- AI分析结果展示
- 系统状态监控
- 统计信息面板

### API接口
- `GET /` - 主页面
- `GET /video_feed` - 视频流
- `GET /api/status` - 系统状态JSON

## 🔧 故障排除

### 常见问题

1. **摄像头连接失败**
   ```
   ❌ 检查RTSP地址是否正确
   ❌ 确认摄像头是否在线
   ❌ 尝试降低分辨率或帧率
   ```

2. **VLM模型加载失败**
   ```
   ❌ 确认网络连接正常 (需下载模型)
   ❌ 检查内存是否充足 (推荐8GB+)
   ❌ 检查CUDA环境 (GPU加速可选)
   ```

3. **Web页面无法访问**
   ```
   ❌ 检查5000端口是否被占用
   ❌ 确认防火墙设置
   ❌ 查看控制台错误信息
   ```

### 性能优化

- **GPU加速**: 安装CUDA和PyTorch GPU版本
- **内存优化**: 调整队列大小和缓冲区设置
- **网络优化**: 调整JPEG质量和帧缩放
- **分析频率**: 根据需要调整AI分析间隔

## 📊 技术栈

| 组件 | 技术栈 | 版本 |
|------|--------|------|
| Web框架 | Flask | 2.0+ |
| 视觉处理 | OpenCV | 4.x |
| AI模型 | Qwen2-VL-7B-Instruct | Latest |
| 深度学习 | PyTorch | 2.x |
| 前端 | HTML5/CSS3/JavaScript | - |
| 视频编码 | MJPEG | - |

## 🛡️ 安全注意事项

- **网络访问**: 默认绑定所有接口 (0.0.0.0)，生产环境请限制访问
- **数据隐私**: 注意摄像头数据的隐私保护
- **资源管理**: 监控内存和CPU使用情况
- **日志管理**: 定期清理临时文件和日志

## 📈 扩展功能

可以考虑添加的功能：

- [ ] 用户认证和权限管理
- [ ] 多摄像头支持
- [ ] 录像功能
- [ ] 移动检测
- [ ] 人脸识别
- [ ] 报警通知
- [ ] 数据库存储
- [ ] 云端部署支持

## 🤝 贡献指南

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 📞 联系方式

如有问题或建议，请通过以下方式联系：

- 🐛 [提交Issue](https://github.com/yourusername/webcam-ai-monitor/issues)
- 📧 Email: your.email@example.com
- 💬 讨论: [GitHub Discussions](https://github.com/yourusername/webcam-ai-monitor/discussions)

## 🙏 致谢

- [Qwen2-VL](https://github.com/QwenLM/Qwen2-VL) - 优秀的视觉语言模型
- [OpenCV](https://opencv.org/) - 计算机视觉库
- [Flask](https://flask.palletsprojects.com/) - Python Web框架

---

⭐ 如果这个项目对你有帮助，请给个star支持一下！

**版本**: v1.0.0
**更新时间**: 2026-03-16
**Python兼容性**: 3.8+