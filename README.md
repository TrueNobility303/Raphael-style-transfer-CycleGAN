# Raphael-style-transfer-CycleGAN

## 摘要

在CycleGAN的基础上，对其进行一定程度的改进，将其运用于Raphael风格迁移任务。

CycleGAN源代码对于小样本风格迁移（只有36张风格图片，8张内容图片—）的表现不佳。

为了优化CycleGAN的表现，改动了训练策略，并且经过对比试验后改进了Patch Discriminator的感受野（Patch大小），使得生成的图片既不至于像照片一样精细，又不至于过于抽象而难以理解，使生成的图片正好位于画的范畴之内。

同时，为了直面小样本的问题，尝试使用单一风格图片和单一内容图片进行CycelGAN的训练。在不使用任何数据扩增的前提下，我们采用了一些经典GAN模型中的策略，解决小样本CycleGAN训练问题。

对于单一风格图片的训练，引入SinGAN的思想和训练方法，使用多尺度的CycleGAN构成整体网络。并且尝试了三种训练多尺度网络的训练策略。

对于单一内容图片的训练，引入Patch Permutation GAN中的Patch Permutation模块。


## 文件说明

代码结构和CylceGAN源代码相同，对于改进的代码部分，详见myCycleGAN的README文件。

## 运行说明


使用优化后的CycleGAN模型训练
```
./myCycleGAN/train.py --dataroot {$PATH} --name {$NAME} --gpu_ids {$ID}
```

引入Patch Permutation 模块训练针对单一风格图片的风格迁移模型
```
./myCycleGAN/train_p2gan.py --dataroot {$PATH} --name {$NAME} --gpu_ids {$ID}
```

引入SinGAN的思想训练单一内容图片的风格迁移模型,但训练策略与原SinGAN不同，采用端到端的训练策略
```
./myCycleGAN/train_singan.py --dataroot {$PATH} --name {$NAME} --gpu_ids {$ID}
```

引入SinGAN的思想训练单一内容图片的风格迁移模型,但引入层级的特征融合模块（FFM），以使模型同时获得高尺度的内容信息和低尺度的风格信息
```
./myCycleGAN/train_higan.py --dataroot {$PATH} --name {$NAME} --gpu_ids {$ID}
```

引入SinGAN的思想训练单一内容图片的风格迁移模型,训练方式与原SinGAN相同，当每一尺度的GAN训练完后固定其参数，进行更高尺度的训练
```
./myCycleGAN/train_fixgan.py --dataroot {$PATH} --name {$NAME} --gpu_ids {$ID}
```

