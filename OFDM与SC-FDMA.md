# OFDM
OFDM用于LTE系统下行数据传输
## OFDM实现方式
OFDM的本质就是发送端用待调制的数据对一系列复指数信号进行加权，合成一个复信号，利用IQ调制发送出去，接收端通过IQ解调恢复出复信号，求出加权系数，也就是傅里叶系数，就得到了调制数据。
### 输入
例如QPSK码流，可视作有四种symbol。
### 调制
s1: 串转并，并行路数计为N，即N个symbol并行处理\
s2: 进行载波调制，对应第k个symbol的离散时间采样后第k个子载波表达式为$`e^{j{2\pi}kn/N} `$ \
需要注意的是，在连续时间条件下，第k个载波表达式为 $\phi_k(t) = e^{j2{\pi}{f_k}t} $，其中$`f_k`$表示其载频率，其表达式为$`k/N{T_s}`$，**$`{T_s}`$为输入码流的每个symbol的时长**，可以观察到由于串转并，到了OFDM中单个OFDM符号的时长为$`NT_s`$ \
s3: 将各路正交载波调制后信号叠加，获得OFDM信号（通过叠加表达式可见其与IDFT表达式相同）,这属于**形式类似** 。
## 保护间隔
采用循环前缀（CP， Cyclic Prefix），信号的后面一部分移到前面（本来是空白的地方），循环前缀的具体原理可以参考文章https://zhuanlan.zhihu.com/p/334754707，本质上是 **将线性卷积转换为圆卷积**。

# SC-FDMA
SC-FDMA用于LTE系统上行数据传输，具体内容可参考文献Single Carrier FDMA for
Uplink Wireless Transmission 和https://support.ixiacom.com/sites/default/files/resources/whitepaper/sc-fdma-indd.pdf
## SC-FDMA实现方式
SC-FDMA与OFDM的主要不同在于DFT mapper, $N$ 个symbol
组成一个block，然后进行$N$点DFT，从而时域信号转为频域，后续进行类似OFDM的处理，子载波数量记为$`M`$ 且$M > N$\
对于OFDM信号，每个symbol对应一个子载波，而SC-FDMA由于DFT的预处理，将一个symbol在频域上拆分，拆分后的信号载映射到其对应的子载波上，映射方式分为locally mapping（集中映射到一段频带）和distributed mapping（分散映射到整个频带上）
## 峰均功率比（PAPR）
SC_FDMA更低，对于发射机要求更低，简单来说N点iFFT将导致PAPR升高N倍（平均功率变为1/N）,FFT降低N倍，由于SC-FDMA有FFT的过程，所以其PAPR相较于OFDM更低。





