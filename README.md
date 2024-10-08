# Collection of Train, Test and Deployment issues about YOLOv5


<details>
  <summary>Imbalance of foreground-background & foreground-foreground</summary>
  如果数据集中背景图片占主导，或目标类别严重不平衡，可以在训练时加入`--image-weights`选项，它将计算每张图片的采样权重：

  1. 统计数据集中所有目标框的 __逆类别频率__
  2. 在epoch开始前，使用上一次验证集上的每类map加权数据集的逆类别频率：`逆类别频率 * (1 - maps) ** 2 / 总类别数`
  3. 统计每张图片的 __类别频率__
  4. 用第2步加权后的逆类别频率对每张图片的类别频率进行加权求和，得到每张图片的权重
  5. 对数据集进行加权采样，结果是训练每个epoch的图片都会发生变化，频率越低、验证集效果越差的类别越容易被采样到，目标框数量越多的图片越容易被采样到
</details>
