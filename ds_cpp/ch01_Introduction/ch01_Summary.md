# 第一章 绪论

## 1.计算机与算法
- 背景 : 1946年 ENIAC 开启了现代电子数字计算机的时代, 计算机科学诞生, 其核心是研究计算方法与过程的规律和技巧, 不仅仅是计算机本身, 其中计算机是帮助计算和解决问题的工具. 
> 古埃及12段直角法的绳索 和 欧氏几何中的尺规都可视为一种计算机, 根据问题使用工具求解问题的步骤可视为算法

- 算法定义 : 基于特定的计算模型(计算工具), 为了解决某一个信息处理问题而设计的一个指令序列
- 算法的 5 种基本特性:  
	- 输入输出
	- 确定性
	- 可行性 
	- 有穷性  
> 针对有穷性引入 Hailstone 问题 (PTA 3N+1 问题) 发现尚未证明其有穷性, 因此得出 程序 $\neq$ 算法  程序仅是一组计算机可以执行的指令, 在符合算法+数据结构的要求下才能正确解决问题

- 评价算法好坏标准 :
	- 正确性 与 高效型(关键)
   	- 健壮性 与 鲁棒性 
   	- 可读性 
   	- 重用性

## 2.复杂度度量
- 算法分析分为两个方面 :
   - 证明正确性
   - 运行时间空间的复杂度度量.
> 任何一次算法中, 存储所消耗的空间都不会多于基本操作次数, 所以只注重于时间的空间度量

- 使用渐进分析(asymptotic analysis)的原因 : 
	- 对于 用算法A来解决具体事件 $p$ 的度量 $T_A(p)$ 因具体事件变化而频繁改变 
	- 对于归纳和划分等价类 用针对事件规模 $n$ 的度量$T_A(n)$ 因输入规模不一而改变
	- 最终引入渐进分析
- 渐进分析定义 : 注重时间复杂度总体的变化趋势和增长速度的分析策略与方法. 通常关注最坏情况 , 其中通用 3 种记号 :
   - $T(n) = O(f(n))$ : $n\rightarrow\infty,\exist正整数c,有T(n)\leq c f(n)$
   - $T(n) = \Omega(f(n))$ : $n\rightarrow\infty,\exist正整数c,有T(n)\geq c f(n)$
   - $T(n) = \Theta(f(n))$ : $n\rightarrow\infty,\exist正整数c_1,c_2,有c_1f(n)\leq T(n) \leq c_2f(n)$
   - 2 种性质: 忽略常数项 忽略低次项  
- 评价模型 : 从复杂的机器和语言类型等抽象出一个理想的模型进行评价, 忽略次要因素 :
    - 图灵机 : 
        - 有限长的纸带
        - 有限种类的字符表
        - 读写头
        - 状态
        - 函数 (状态q, 字符c, 新字符d, 转向L/R, 新状态p(h为终止状态)) 
    - RAM(Random Access Machine) : 
        - 无限的寄存器
        - 固定的指令 如 寻址指令 判定指令 转向指令 (类似汇编指令)

## 3.度量尺度
> 由于c++高级程序语言在一定程度上等价于RAM模型可以通过代码来大致估算时间复杂度

1. 高效解:
   - $O(1)$ : 常数项复杂度, 与输入规模无关
   - $O(logn)$ : 对数复杂度, 不标明底是因为底可以互相转换比如
```c++
/*计算非负整数二进制位数中1的个数*/
int countUintOnes(unsigned int n){
    int sum = 0;
    while(n>0){
        sum+=(1&n);
        n>>=1;
    }
    return sum;
}
```

2. 有效解:
- $O(n)$ : 线性复杂度
- $O(n^c)$ : 多项式复杂度 比如
```c++ 
/*冒泡排序 O(n^2)*/
void bubbleSort(int a[], int n){
    for (bool sorted = false; sorted = !sorted; n--)
        for (int i = 1; i < n; ++i){
            if (a[i - 1] > a[i]){
                std::swap(a[i - 1], a[i]);
                sorted = false;
		}
	}
}
```

3. 难解 : 
- $O(2^n)$ : 指数复杂度 随n增长极快 比如
```c++
/*计算2^n n的二进制长度为r 有n<2^r O(n) = O(2^r)*/
__int64 power(int n){
    __int64 pow = 1;
    while(0<n--){
        pow<<=1;
    }
    return pow;
}
/*
可以发现 针对不同的输入规模 n 或者 r 其时间复杂度不同,
对应的 n 的数值为基准的复杂度为 O(n)
但从另一个角度来说 以 n 的比特位数作为基准则为 O(2^r)
后者为 伪复杂度 
*/
```

- $NPC$问题 : 不存在多项式时间内解决的方法 比如 Subset Problem(美国选举票数问题)

4. 增长速度 : 
$$O(1),O(loglogn),O(logn),O(\sqrt{n}),O(n),O(nloglogn),O(nlogn),O(n^2),O(n^c),O(2^n)$$ 
> 注意 n 足够大 , ln(n)的渐进增长慢于任何次数的幂函数x^ϵ

## 4. 算法分析手段
1. 正确性分析
	- 不变性: 拿冒泡排序举例,不变性在于经过k轮扫描,最大的k位数必然就位
    - 单调性: 拿冒泡排序举例,单调性在于经过k轮扫描,问题规模必然缩减至n-k
2. 迭代
    - 迭代定义 ：用变量的原值推算出新的值，比如循环
    - 迭代分析 : (通过计算循环中的次数)  
		- 算数级数 : $\sum_{k=0}^{n}k=O(n^2)$
     	- 幂级数 : $\sum_{k=0}^{n}k^d\approx\int_0^nx^{d+1}{\rm d}x =O(n^{d+1})$
        - 几何级数 : $\sum_{k=0}^{n}a^n = O(a^n)$
        - 收敛级数 : 先判断为收敛级数 , 比如 $\sum_{k=1}^{n}\frac{1}{2^k}=O(1)$
        - 调和级数 : $\sum_{k=1}^n\frac{1}{k}=\Theta(logn)$
        - 对数级数 : $\sum_{k=1}^nlog(k)=\Theta(nlogn)$
        - 或者 通过画出xy轴图像来判断
3. 递归 
   - 递归定义 ：将问题分为若干个问题调用自身来解决
   - 基本要素 ：
     - 递归基 : 针对多种退化可能会含有多个递归基和隐藏递归基
     - 多向 : 根据规模选择递归方式如
        ```
        /*计算2^n O(r)*/
            __int64 power(int n){
                if(0 == n ) return 1;
                if(n & 1)
                    return sqr(power(n>>1))<<1;//奇数
                else
                    return sqr(power(n>>1));//偶数
            }
        ```
     - 减少成本 : 通过栈来模拟递归,消除操作系统的的创建递归栈 或者 通过尾递归(最后的递归都终止于递归调用)转变成迭代比如**递归颠倒数组算法**变成迭代版本
   - 分析方法 :
      - 递归跟踪 : 画出递归树
      - 递归方程 : 求出递归方程最后的和
   - 递归类别 : 
      - 减而治之 ：线性递归 如 **~~数组求和~~**每次将规模分为 1 和 n-1 (解递归方程的窍门 通过-n 凑出T(n)-n 形式)
      - 分而治之 ：将问题分成互不重合的若干个小问题如
        ```
        /*
        分治求sum
        画出递归树发现是 2^log(n+1)-1 = O(n)
        */
            int sum(int a[],int low ,int high){
                if(low==high) return a[low];
                int mi = (low+high)>>1;
                return sum(a,low,mi) + sum(a,mi+1,high);
            }
        ```
        > 如果 若干问题重合会产生复杂度无谓的增加比如 **~~fib二分~~**
        > 两个知识点 如何求出 S(n) = fib(n+1) = ($\frac{\Phi^{n+1} - \hat{\Phi}^{n+1}}{\sqrt{5}}$) = $O(\Phi^n)$
    - 动态规划 :
      - 递归形式 记忆法
      - 迭代形式 状态转移方程
      - 举例如
        ```
        求解第n个fib数 o(n) 推得求解数列 将o(2^n)降到了o(n^2) 
        int fib(int n){
            int f = 0 , g = 1;
            while(n--){
                g+=f;
                f=g-f;
            }
            return f;
        }
        ```
4. 封底估算
   - $一天 \approx 10^5s$
   - $半生 \approx 1.6\times10^9s$
   - $一生 \approx 3\times10^9s$
   - $三生三世 \approx 10^{10}s$
   - $宇宙至今 \approx 10^{21}s$
   - $10^9flo\approx 1s$
   - 注意灵活运用幂指数等价来快速封地估算

5. 抽象数据类型
   - ADT = 数据模型和定义在模型上的一组操作
   - DS = 基于某种特定语言,实现ADT得一整套算法
   - 理解 :
     - abstrct data type 类比 整型
     - data struct 类比 int a; 中的 a
     - 可以把数据结构称作抽象数据类型的实例化 或者 抽象数据类型称做抽象数据结构

6. 补充问题 
   - 分治法找 **递归/迭代求数组最大两个值的下标**
   - 动态规划 **LCS 问题** $O(\frac{2n!}{n!n!})$->$O(m\times n)$ 
   - 取最优例子 低效例子一笔带过