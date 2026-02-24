# Multifunctional-Metalens-Design-Simulation 3-Bit-Edition
This project is a comprehensive, Python-based toolkit for the design, simulation, and layout generation of multifunctional metalenses and metasurfaces.
Whether you are conducting research in micro/nano-optics or engineering metasurface devices for fabrication, this script provides an end-to-end workflow: from target phase calculation and unit cell library matching to GDSII physical layout export and focal field simulation.
In the V3 release, we have introduced a core 3-Bit Phase Quantization (8-level discretization) architecture, which significantly reduces fabrication difficulty and improves design robustness.
<img width="5682" height="3541" alt="all_phase_distributions" src="https://github.com/user-attachments/assets/666906f4-aae2-4a56-bd9e-a88a1beda16b" />
<img width="1742" height="981" alt="image" src="https://github.com/user-attachments/assets/e947c3f4-16a0-4ebf-b8c9-78631a07b618" />

✨ Core Features
1. 🎯 15+ Target Light Field Modulation Modes
The script features multiple analytical phase formulas and iterative phase calculations based on the GS (Gerchberg-Saxton) algorithm. You can easily switch the focus_type to generate the following target light fields:
Basic Focusing: Point focus (point), Line focus (line)
Vortex & Non-diffracting Beams: Vortex beam (vortex), Bessel beam (bessel), Airy beam (airy), Bessel-vortex composite (bessel_vortex)
Multi-focus & Aberration Control: Off-axis focusing (off_axis), Transverse multi-focus (multi_focus), Astigmatic lens (astigmatic), Spiral multi-focus (spiral_multi_focus), Longitudinal multi-focus (longitudinal_multi_focus), Longitudinal vortex (longitudinal_vortex)
Complex Fields & Holography (GS Algorithm): Optical lattice (optical_lattice), Flat-top beam shaping (flat_top_gs), Custom holographic patterns (holographic_gs)


2. 🚀 [Core Update] 3-Bit Phase Quantization Mode
By toggling the ENABLE_3BIT_QUANTIZATION switch, you can freely choose between continuous matching and discrete quantization modes:
Continuous Matching Mode (False): Searches the full-size unit cell library for the nanopillar that most closely matches the required phase for each pixel, aiming for extreme theoretical phase accuracy.
3-Bit Quantization Mode (True): Evenly divides the continuous phase (0 to 2π) into 8 standard steps (0°, 45°, 90°... 315°). The algorithm automatically pre-selects 8 standard nanopillar sizes from the library that best fit these ideal phases, and populates the entire array using only these 8 unit cells.
Advantage: Greatly reduces the proximity effect in Electron Beam Lithography (EBL), minimizes processing data size, and improves the fault tolerance and yield of large-area array fabrication.
<img width="1466" height="1251" alt="image" src="https://github.com/user-attachments/assets/b8dc7c61-be16-4186-ab61-73edc97bdeb7" />


4. 🏭 Industrial-Grade GDSII Layout Generation
Built on the gdspy library, it automatically generates a .gds layout file based on the phase mapping results, ready for photomask making or EBL exposure.
Supports customizable array dimensions (nx, ny), unit cell pitch (pixel_pitch), and operating wavelength (lam_nm).

5. 🔬 Rapid Focal Field Simulation & Visualization
FFT Focal Field Calculation: Built-in 2D focal plane optical field intensity calculation based on Fast Fourier Transform to instantly verify the lens design.
Multi-dimensional Visualization: One-click generation of comparative views, intuitively displaying Target Continuous Phase vs. Mapped Nanopillar Radius vs. Quantized Actual Phase, making it easy to troubleshoot design blind spots.

6. 🛠️ Flexible Unit Library Interface
Real Library Mode: Supports reading pre-calculated CSV unit library files (containing radius, phase, and amplitude) obtained from FDTD/RCWA parameter sweeps.
Virtual Library Mode: In the absence of real simulation data, the script will automatically generate a virtual test library with random amplitudes and linear phases, ensuring the code can run immediately in any environment to verify algorithmic logic.
<img width="1600" height="647" alt="image" src="https://github.com/user-attachments/assets/e38c8f20-75ee-4828-9720-5f83f88764de" />

📂 Output Files
After each run, the system generates an independent set of files in the specified output directory (Desktop by default), suffixed with your parameters. For example, a 3-bit quantized design for a 630nm vortex beam will output:
vortex_630nm_3bit.gds: Layout File. Used for micro/nano fabrication.
vortex_630nm_3bit_placements.csv: Placement Coordinate Table. Details the (x, y) coordinates, target phase, actual phase, mapped radius, and quantization level for each unit cell.
vortex_630nm_3bit_phase.png: Phase Analysis Plot. Pseudocolor plots containing the target phase, radius layout, and actual stepped phase.
vortex_630nm_3bit_focus.png: Focal Plane Light Field Plot. Simulates and displays the intensity distribution at the target focal length.
vortex_630nm_3bit_meta.json: Metadata File. Records the parameters and paths of this generation for easy data tracing.

Ensure you have the following Python libraries installed before use:
pip install numpy pandas matplotlib gdspy

My email：a502820856@gmail.com

:)

中文翻译
多功能超表面设计仿真程序（3bit版本）
本项目是一个基于 Python 的多功能超构透镜（Metalens）设计、仿真与版图生成工具。无论您是从事微纳光学研究，还是进行超构表面器件的工程化流片，本脚本都能为您提供从目标相位计算、单元库匹配到 GDSII 物理版图导出及焦场仿真的一站式端到端工作流。
在 V3 版本中引入了 3-Bit 相位量化（8阶离散化） 架构，极大降低了加工难度并提高了设计的鲁棒性。
<img width="5682" height="3541" alt="all_phase_distributions" src="https://github.com/user-attachments/assets/666906f4-aae2-4a56-bd9e-a88a1beda16b" />
<img width="1742" height="981" alt="image" src="https://github.com/user-attachments/assets/e947c3f4-16a0-4ebf-b8c9-78631a07b618" />
✨ 核心功能亮点


🎯 支持多达 15 种丰富的光场调控模式
脚本内置了多种解析相位公式与基于 GS (Gerchberg-Saxton) 算法的迭代相位计算，支持一键切换 focus_type 生成以下目标光场：
基础聚焦：点聚焦 (point)、线聚焦 (line)
涡旋与无衍射光束：涡旋光束 (vortex)、贝塞尔光束 (bessel)、艾里光束 (airy)、贝塞尔-涡旋复合光束 (bessel_vortex)
多焦点与像差调控：离轴聚焦 (off_axis)、横向多焦点 (multi_focus)、像散透镜 (astigmatic)、螺旋多焦点 (spiral_multi_focus)、轴向多焦点 (longitudinal_multi_focus)、轴向多涡旋 (longitudinal_vortex)
复杂光场与全息 (GS算法)：光学晶格 (optical_lattice)、平顶光束整形 (flat_top_gs)、自定义全息图案 (holographic_gs)


🚀 [核心更新] 3-Bit 相位量化模式 (3-Bit Quantization)通过切换 ENABLE_3BIT_QUANTIZATION 开关，自由选择连续匹配或离散量化模式：连续匹配模式 (False)：在全尺寸单元库中为每个像素寻找相位最接近的纳米柱，追求极致的理论相位逼近。3-bit 量化模式 (True)：将 $0 \sim 2\pi$ 的连续相位均匀划分为 8 个标准阶梯（0°, 45°, 90°... 315°）。算法会自动从库中预选出最贴合这 8 个理想相位的 8 种标准纳米柱尺寸，全阵列仅使用这 8 种单元进行排布。优势：大幅降低电子束曝光 (EBL) 的临近效应，减少加工数据量，提高大面积阵列制备的容错率与良率。
<img width="1466" height="1251" alt="image" src="https://github.com/user-attachments/assets/b8dc7c61-be16-4186-ab61-73edc97bdeb7" />


🏭 工业级 GDSII 版图自动化生成
基于 gdspy 库，根据相位映射结果自动生成可直接用于掩膜版制作或 EBL 曝光的 .gds 版图文件。
支持自定义阵列尺寸 (nx, ny)、晶胞周期 (pixel_pitch) 与工作波长 (lam_nm)。


🔬 快速焦场仿真与可视化
FFT 焦场计算：内置基于快速傅里叶变换的二维焦平面光场强度分布计算，实时验证透镜的设计效果。
多维数据可视化：一键生成对比视图，直观展示 目标连续相位 vs 映射后纳米柱半径分布 vs 量化后实际相位，方便排查设计死角


🛠️ 灵活的单元库 (Unit Library) 接口
真实库模式：支持读取基于 FDTD/RCWA 扫描预计算好的 CSV 单元库文件（包含半径、相位、振幅）。
虚拟库模式：在缺少真实仿真数据时，脚本会自动生成一个具有随机振幅和线性相位的虚拟测试库，保证代码在任何环境下都能立即跑通并验证算法逻辑。
<img width="1600" height="647" alt="image" src="https://github.com/user-attachments/assets/e38c8f20-75ee-4828-9720-5f83f88764de" />

📂 输出文件清单每次运行脚本后，系统将在指定的输出目录（默认桌面）生成带有参数后缀的独立文件集，例如针对 630nm 涡旋光束的 3-bit 量化设计，将输出：
vortex_630nm_3bit.gds: 版图文件。用于微纳加工。
vortex_630nm_3bit_placements.csv: 排布坐标表。详细记录每个单元的 $(x, y)$ 坐标、目标相位、实际相位、映射半径与量化等级。
vortex_630nm_3bit_phase.png: 相位分析图。包含目标相位、半径排布与实际阶梯相位的伪彩图。
vortex_630nm_3bit_focus.png: 焦平面光场图。仿真并展示目标焦距处的强度分布。
vortex_630nm_3bit_meta.json: 元数据文件。记录本次生成的参数与路径，方便数据追溯。


使用前请确保已安装以下 Python 库：
pip install numpy pandas matplotlib gdspy

与我联系：a502820856@gmail.com
