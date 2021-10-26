### 复现OpenPCDet

- Properties
Python3.7.10
torch1.3.0
CUDA Version 10.1.105
- 查看cuda版本
nvcc --version
cat /usr/local/cuda/version.txt(这个不准)
nvidia-smi右上角的是驱动的版本
- 查看pytorch版本
运行python
import torch
torch.__version__
- 创建虚拟环境&安装torch
conda create -n OpenPCDet python=3.7
conda activate OpenPCDet
https://blog.csdn.net/CS_Whale/article/details/114934876
https://download.pytorch.org/whl/torch_stable.html
下载这个cu101/torch-1.3.0-cp37-cp37m-manylinux1_x86_64.whl
pip install torch-1.3.0-cp37-cp37m-manylinux1_x86_64.whl
运行python
import torch
torch.cuda.is_available()
显示True说明torch和cuda版本对应上了

- 安装spconv
https://github.com/traveller59/spconv
https://sirjamie.github.io/2020/10/19/OpenPCDet/
https://www.fatalerrors.org/a/openpcdet-installation-and-quick-demo.html
cmake版本3.13.2，已经装好了（添加到PATH这步不用管）
进入目录，注释整行，我没做这步。
执行python setup.py bdist_wheel这步没有报错
cd dist
ls一下
pip install spconv-1.2.1-cp37-cp37m-linux_x86_64.whl
这就安装好spconv1.2了
验证：python    import spconv


- 继而安装OpenPCDet
git clone https://github.com/open-mmlab/OpenPCDet.git
cd OpenPCDet
然后这步
pip install -r requirements.txt
会把你的torch1.3.0卸载，然后安装torch1.9(最新版pytorch)
这就会导致与cuda版本不匹配。
于是我重新安装torch1.3.0，这会自动卸载torch1.9
会报错：torchvision  kornia  版本不匹配，这都是因为requirements.txt使得安装版本都是最新版。
解决方法：

- torchvision
pip install --no-deps torchvision==0.4.1（见后文对应关系）
python
import torchvision
torchvision.__version__
0.4.1

- kornia
https://github.com/kornia
https://pypi.org/project/kornia/
在官网上点release history查看过去的版本，并找到与pytorch的对应关系

- 然后应该版本就都匹配上了，最后一步到OpenPCDet目录下运行
python setup.py develop
完成pcdet==0.3.0+0的安装
验证：python    import pcdet

- 对应关系
torchvision
https://pypi.org/project/torchvision/
https://blog.csdn.net/lxx4610/article/details/101020815
kornia
https://pypi.org/project/kornia/0.4.0/

- linux软连接及其删除
https://www.cnblogs.com/sueyyyy/p/10985443.html
https://blog.csdn.net/chenghuikai/article/details/50961622

- 运行demo
https://panfake.com/2020/03/qxcbconnection-could-not-connect-to-display/
https://zhuanlan.zhihu.com/p/131558897

- 运行train.py的有关road_plane报错
https://github.com/open-mmlab/OpenPCDet/issues/473
通过下载那个option的文件解决了（但是没有重新生成data infos）

- 解压tar/tgz
https://www.cnblogs.com/cap-rq/p/11457446.html
https://zhidao.baidu.com/question/9844116.html

