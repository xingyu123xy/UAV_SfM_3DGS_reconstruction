# UAV_SfM_3DGS_reconstruction
UAV aerial 3D reconstruction based on SfM + 3DGS, including camera pose conversion and CUDA rendering optimization for drone surveying scenes. 基于SfM+3DGS的无人机航拍三维重建，包含相机位姿格式转换与面向航测场景的CUDA渲染性能优化。

项目简介：
本项目面向无人机倾斜摄影测绘场景，设计一套「SfM空三解算+3DGS隐式重建」完整管线。针对航拍大场景存在显存占用过高、植被/建筑立面弱纹理空洞、推理速度慢等痛点，基于CUDA完成渲染算子轻量化优化。

整体技术链路：航拍影像GPS辅助SfM稀疏重建 → C++位姿格式转换 → 3D高斯泼溅神经重建 → GPU并行加速推理。

技术栈
C++、CUDA C、Python
COLMAP、Nerfstudio、SfM-MVS多视图几何、PCL、OpenCV

规划实现流程
1. 数据预处理：公开无人机航测数据集筛选，利用影像GPS先验约束空三优化；
2. 增量式SfM重建：基于COLMAP完成特征匹配、BA光束平差，输出相机内外参与全局轨迹；
3. 跨框架位姿转换：研究C++工具，将COLMAP输出参数标准化为3DGS训练输入格式；
4. 航拍场景3DGS训练：基于Splatfacto模型完成大场景隐式重建；
5. CUDA性能优化：改写光栅化渲染内核，降低显存开销、提升实时渲染速度；
6. 定量对比实验：对比传统MVS稠密重建与优化后3DGS的几何误差、显存、耗时指标。
