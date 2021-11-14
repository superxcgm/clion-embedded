# 如何点亮LED灯？

## 环境

* 板子：STM32F072 Discovery kit
* 芯片：STM32F072RBT6
* 开发机：macOS Catalina 10.15.7
* IDE：CLion2021.1

## 需要的软件

* OpenOCD（用于调试）
* st-link（用于下载程序）
* arm-gcc编译器
* STM32CubeMX（用于生成工程）

前三个可以通过`install-tools.sh`自动安装，STM32CubeMX需要去[ST的网站](https://www.st.com/en/development-tools/stm32cubemx.html)下载。CLion需要安装插件Embedded Development Support，和在`Preferences=>Build, Execution, Deployment=>Embedded Development`下配置好OpenOCD和STM32CubeMX的位置。

## 生成工程并点亮LED

1. 打开STM32CubeMX，选择board，STM32F072B-DISCO，双击就可以进入项目配置。

2. 在Project Manager的页面下，填写项目的名称和选择Toolchain/IDE为SW4STM32，然后点击右上角的GENERATE CODE生成代码。

3. 使用CLion打开项目，选择stm32f0discovery.cfg，CLion会自动生成`CMakeLists.txt`。然后点右上角的build，应该可以正常构建。

4. 在main函数里面的while循环中加入如下代码，用于点亮LED

   ```c
   HAL_GPIO_WritePin(LD3_GPIO_Port, LD3_Pin, GPIO_PIN_RESET);
   HAL_Delay(500);
   
   HAL_GPIO_WritePin(LD3_GPIO_Port, LD3_Pin, GPIO_PIN_SET);
   HAL_Delay(500);
   ```

5. 将板子连接电脑，注意，需要连接的是板子上的USB ST-LINK的口。点击CLion右上角的Run，代码就会被编译并烧录到板子上。板子上回旋镖的LD3会闪烁，说明我们的程序正常在板子上运行起来了。

