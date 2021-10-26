## anaconda prompt里安装mayavi(mayavi.mlab)
### background
conda install mayavi
import mayavi不报错
from mayavi import mlab报错
### relevant useful websites & potential solutions
https://zhuanlan.zhihu.com/p/385308168
https://blog.csdn.net/Papaya_shun/article/details/106926136
https://stackoverflow.com/questions/53853254/install-mayavi-for-python-3-7-1-in-windows-10
### my solution
```
conda create -n mayavi python=3.6
conda activate mayavi
conda install -c conda-forge mayavi
# 就这一句就解决问题了，应该是不需要从轮子装。
```
### test
```
import numpy as np
from mayavi import mlab
x, y = np.ogrid[-2:2:20j, -2:2:20j]
z = x * np.exp( - x**2 - y**2)
pl = mlab.surf(x, y, z, warp_scale="auto")
mlab.axes(xlabel='x', ylabel='y', zlabel='z')
mlab.outline(pl)
mlab.show()
```
### install open3d(安装在st3d这个虚拟环境了)
http://www.open3d.org/docs/release/getting_started.html
https://pypi.org/project/open3d/
```
conda install -c open3d-admin -c conda-forge open3d
```