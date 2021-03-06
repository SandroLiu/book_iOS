# 进制与位运算

## 进制

1. 10进制，%d输出
    int num = 12;
2. 八进制，在前面加上一个0就代表八进制，%o输出
    int num1 = 014;
3. 十六进制，在数值前面加上一个0x就代表十六进制，%x输出
    int num2 = 0xc;
4.  二进制，在数值前面加上0b就代表二进制，%d输出
    int num3 = 0b1100

## 原码反码补码

计算机中存储的是数据的补码
- 正数的原码就是它的反码和补码
- 负数的反码，符号位不变，其它取反
- 负数的补码，反码+1

## 位运算

1. 按位与
    - 只有对应的两位都是1才返回1，否则返回0
    - 一假则假
    - 任何数按位与上1结果还是那个数

    ```objc
     1001
    &0101
     _______
     0001
      1001
     &1111
     ______
      1001

    ```
2. 按位或
    - 对应的两位中一位是1结果就为1
    - 一真则真
3. 按位异或
    - 对应的两位不相同结果是1，相同则为0
    - 多个整数按位异或的结果和顺序无关
    - 相同整数按位异或的结果是0
    - 任何整数按位异或上0结果不变
    - 任何整数按位异或上另一个整数两次结果还是那个数
4. 按位取反
    - 0变1，1变0
5. 左移右移
 -  左移
    - a << n 把整数a的二进制位往左边移n位
    - 移除的位砍掉，低位补0
    - 左移的应用场景：当要计算某个数乘以2的n次方的时候就用左移，效率最高
    - 左移有可能改变数值的正负性
 - 右移
    - a >> n
    - 移出的位砍掉，缺少的，最高位是0就补0，最高位是1就补1
    - 应用场景：当要计算某个数除以2的n次方的时候就用右移

## 位运算练习
1. 输出一个整数的每个二进制位
2. 判断一个数的奇偶性
3. 交换两个变量值
4. 简单加密

##0xFF
0xFF的二进制是1111 1111，一个十六进制位等于4个二进制位
