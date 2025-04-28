# Pymol教程
***
## 1. Pymol安装
### 安装包安装
<https://pymol.org>
### conda安装
conda create --name myenv python=3.10  
conda activate myenv\
conda install -c conda-forge -c schrodinger pymol-bundle
### 安装许可证（教育版）
## 2. 常用命令集成面板
### Action
包含放大（zoom）、与xyz坐标轴对齐（orient）、自动优化分子结构（clean）、展示方式（present 可显示蛋白质配体结合口袋）、相互作用（find）删除（delete object）加氢去氢（hydrogen）、复制（copy）、提取（extract）计算原子总数、电荷、表面积、分子质量（compute）等操作
### Show
改变选中原子的显示方式，有线型（lines）、球（spheres）、棍（sticks）、飘带（ribbons）卡通（cartoon）、点状表面（dots）、网格表面（mesh）、实体表面（surface）
### Hide
隐藏选中对象的表示方式
### Label
为对象绘制文本标签
### Color
设置选中对象的颜色
## 3. Pymol绘图示例
### 1. 蛋白质配体相互作用
![Picture1](https://github.com/binz222/Pymol/blob/main/ProLig.png)
#### 准备工作
将背景颜色设置为白色  
**bg_color white** Display > Background > White
载入蛋白\
**fetch 1l7f** File > Get PDB File > PDB ID: 1l7f\
删除多余原子并复制蛋白结构\
**remove not (polymer | resi 801)** Sequence > remove\
**create pro, polymer** A > Copy to object, rename
#### 绘制结合口袋相互作用
提取配体、重命名并更改颜色  
**extract lig, resi 801** A > extract object, rename\
**color yellow, lig & name C\*** C > by element\
提取氢键残基并更改颜色\
**extract HBres, resi 118+151+227+178+152+292+371** A > extract object, rename\
**color pink, HBres & name C\*** C > by element\
隐藏卡通展示
**hide cartoon** H > cartoon\
将配体与残基显示为棍状模型并放大\
**show sticks,lig | HBres** S > sticks\
**zoom lig | HBres** A > zoom \
标记残基名及编号并设置字号\
**label HBres and name CA, resn+resi** L > residues\
**set label_size,30** Setting > Label > Size\
绘制氢键相互作用并更改颜色\
**distance /HBres/A/A/ARG\`371/NH1, /lig/G/A/BCZ\`801/O7** Wizard > Measurement\
**color green, dist\*** C > green\
将蛋白以卡通展示并设置颜色、透明度\
**show cartoon, 1l7f** S > Cartoon\
**color gray90, 1l7f** C > gray90\
**set cartoon_transparency, 0.2** Setting > Trsnaparency > Cartoon > 20%\
光线追踪\
**ray**\
输出图片\
**png PL.png，dpi=300** File > Export Image As > Png
#### 绘制全局图
隐藏\
hide\
将蛋白以实体表面展示并更改颜色\
show surface, pro\
color gray90, pro\
将配体以棍状模型展示\
show sticks,lig\
缩放\
zoom pro\
光线追踪\
ray\
输出图片\
png 2.png, dpi=300
### 2. 分子轨道
![Picture2](https://github.com/binz222/Pymol/blob/main/or.png)\
获取cube文件及mol2文件  
formchk Int0.chk Int0.fchk\
File > Open > Int0.fchk\
Tools > MOs > Visualize > Update\
Results > Surfaces/Contours > Cube Actions > Save Cube\
File > Save > Int0.mol2
****
载入构象\
load Int0.mol2\
展示方式改为Houkmol\
set valence, 0\
hide everything\
show sticks\
show spheres\
show labels\
show dashes\
set stick_radius, .07\
set sphere_scale, .18\
set sphere_scale, .13, elem H\
set bg_rgb=[1, 1, 1]\
set stick_quality, 50\
set sphere_quality, 4\
color gray85, elem C\
color red, elem O\
color slate, elem N\
color gray98, elem H\
set stick_color, black\
set ray_trace_mode, 1\
set ray_texture, 2\
set antialias, 3\
set ambient, 0.5\
set spec_count, 5\
set shininess, 50\
set specular, 1\
set reflect, .1\
set dash_color, black\
set dash_gap, .2\
set dash_length, .1\
set dash_round_ends, 0.1\
set dash_radius, .05\
set ray_trace_gain, 10\
set stick_h_scale, 1\
set ray_shadow, off\
set label_size, 60\
set label_distance_digits, 2\
set orthoscopic, on\
载入cube文件\
load Int0_mo95.cub\
创建正负等值面\
isosurface Int0-n, Int0_mo95, -0.02\
isosurface Int1-p, Int0_mo95, +0.02\
设置不透明度\
set transparency, 0.2\
着色\
set surface_color, density, *n\
set surface_color, forest, *p\
光线追踪
ray
### 3. 简单动画制作
<video src="https://github.com/binz222/Pymol/blob/main/1.mp4" autoplay></video>  
隐藏标签  
hide label\
缩放\
zoom\
设置总帧数\
mset 1 x 500\
保存第一帧、最后一帧\
mview store, 1\
mview store, 500\
放大结合口袋并保存该帧\
zoom lig | HBres\
mview store, 100\
向左旋转90°并保存该帧\
turn y, -90\
mview store, 200\
向右旋转90°并保存该帧\
turn y, 90\
mview store, 300\
向右旋转90°并保存该帧\
turn y, 90\
mview store, 400\
播放\
mplay
## 参考文章
http://pymol.chenzhaoqiang.com/intro/basicManual.html  
https://www.shaoqz.cn/2020/06/29/PyMol-Orbital/  
https://zhuanlan.zhihu.com/p/129091849  
https://www.bilibili.com/video/BV1FV4y187DF?spm_id_from=333.788.videopod.sections&vd_source=a250bc4364a198abeb310825910a3646







