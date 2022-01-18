# Collection of Train, Test and Deployment issues about YOLOv5


### 参数初始化

* `Conv2d`: 

  使用pytorch默认的参数初始化
  
  ```python
  # Setting a=sqrt(5) in kaiming_uniform is the same as initializing with
  # uniform(-1/sqrt(k), 1/sqrt(k)), where k = weight.size(1) * prod(*kernel_size)
  # For more details see: https://github.com/pytorch/pytorch/issues/15314#issuecomment-477448573
  init.kaiming_uniform_(self.weight, a=math.sqrt(5), mode='fan_in', nonlinearity='leaky_relu')
  if self.bias is not None:
      fan_in, _ = init._calculate_fan_in_and_fan_out(self.weight)
      if fan_in != 0:
          bound = 1 / math.sqrt(fan_in)
          init.uniform_(self.bias, -bound, bound)
  ```
