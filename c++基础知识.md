1.
特性	   #include <math.h> 	   #include <cmath>
语言风格 	C 风格头文件 	       C++ 风格头文件
命名空间	 全局命名空间	         将函数放在 std 命名空间
重载支持	 有限的函数重载	       更好的函数重载
推荐程度	 兼容 C 语言	           C++ 推荐使用







2.#include <iostream>
using namespace std;
int main() {
    int n;
    cin >> n;
    int pass = 0;   // 及格人数（≥60分）
    int good = 0;   // 优秀人数（≥85分）
    // 边读入边统计，不需要数组
    for (int i = 0; i < n; i++) {
        int score;
        cin >> score;
        if (score >= 60) {
            pass++;
        }
        if (score >= 85) {
            good++;
        }
    }
    
    // 计算百分比并四舍五入（整数运算，避免浮点误差）
    int passRate = (pass * 100 + n / 2) / n;
    int goodRate = (good * 100 + n / 2) / n;
    
    // 输出结果
    cout << passRate << "%" << endl;
    cout << goodRate << "%" << endl;
    
    return 0;
}




3. 小蓝要为一条街的住户制作门牌号。这条街一共有2020位住户，门牌号从1到2020编号。小蓝制作门牌的方法是先制作0到9这几个数字字符，最后根据需要将字符粘到门牌上，例如门牌 1017 需要依次粘贴字符 1、0、1、7，即需1个字符0，2个字符1，1个字符7。请问要制作所有的 11 到 20202020 号门牌，总共需要多少个字符 22？
#include<iostream>
#include<string>
using namespace std;
int main() {
    int count = 0;
    
    // 遍历 1 到 2020
    for (int i = 1; i <= 2020; i++) {
        string num =to_string(i);  // 将数字转为字符串
        // 遍历字符串中的每个字符
        for (int j = 0; j < num.length(); j++) {
            if (num[j] == '2') {
                count++;
            }
        }
    }
    
    cout << count << endl;
    return 0;
}





4.Vector 详细解释
vector 是 C++ 标准模板库（STL）中的一个动态数组容器。它可以根据需要自动调整大小，非常灵活和强大。

🎯 什么是 Vector？
对比：静态数组 vs Vector
cpp
// 静态数组（传统C风格）
int arr[100];        // 大小固定为100，不能改变
arr[0] = 10;         // 可以访问
// 问题：不知道需要多大空间，可能浪费或不够用

// Vector（C++动态数组）
#include <vector>
vector<int> vec;      // 初始为空，可以动态增长
vec.push_back(10);    // 自动扩展，添加元素
// 优点：根据需要自动调整大小
📦 基本操作
1. 包含头文件
cpp
#include <vector>  // 必须包含这个头文件
using namespace std;  // 或者使用 std::vector
2. 声明和初始化
cpp
// 空vector
vector<int> v1;                    // 存储int类型的空vector

// 指定大小
vector<int> v2(10);                // 10个元素，初始值为0
vector<int> v3(10, 5);             // 10个元素，每个都是5

// 使用列表初始化（C++11）
vector<int> v4 = {1, 2, 3, 4, 5};  // 5个元素：1,2,3,4,5
vector<int> v5{1, 2, 3, 4, 5};     // 同上

// 拷贝初始化
vector<int> v6(v4);                 // 拷贝v4的所有元素
3. 常用操作
cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec;
    
    // 添加元素
    vec.push_back(10);   // 末尾添加10: [10]
    vec.push_back(20);   // 末尾添加20: [10, 20]
    vec.push_back(30);   // 末尾添加30: [10, 20, 30]
    
    // 访问元素
    cout << vec[0] << endl;      // 输出：10（不检查边界）
    cout << vec.at(1) << endl;   // 输出：20（检查边界，安全）
    cout << vec.front() << endl; // 输出：10（第一个元素）
    cout << vec.back() << endl;  // 输出：30（最后一个元素）
    
    // 获取大小
    cout << vec.size() << endl;   // 输出：3（元素个数）
    cout << vec.capacity() << endl; // 输出：>=3（容量）
    
    // 判断是否为空
    if (vec.empty()) {
        cout << "vector为空" << endl;
    } else {
        cout << "vector有" << vec.size() << "个元素" << endl;
    }
    
    // 删除元素
    vec.pop_back();      // 删除最后一个元素: [10, 20]
    vec.clear();         // 清空所有元素: []
    
    return 0;
}
4. 遍历 vector
cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    
    // 方法1：使用索引（像数组一样）
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << " ";
    }
    cout << endl;
    
    // 方法2：使用范围for循环（C++11）
    for (int x : vec) {
        cout << x << " ";
    }
    cout << endl;
    
    // 方法3：使用迭代器
    for (vector<int>::iterator it = vec.begin(); it != vec.end(); it++) {
        cout << *it << " ";
    }
    cout << endl;
    
    // 方法4：使用auto简化迭代器
    for (auto it = vec.begin(); it != vec.end(); it++) {
        cout << *it << " ";
    }
    cout << endl;
    
    return 0;
}
🔧 在分巧克力问题中的应用
使用 vector 的版本
cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int N, K;
    cin >> N >> K;
    
    // 创建两个vector，大小由输入决定
    vector<int> h(N);  // N个元素，初始值为0
    vector<int> w(N);
    
    // 输入数据
    for (int i = 0; i < N; i++) {
        cin >> h[i] >> w[i];  // 像数组一样使用
    }
    
    // 二分查找
    int left = 1, right = 100000, ans = 1;
    
    while (left <= right) {
        int mid = (left + right) / 2;
        long long total = 0;
        
        // 遍历vector
        for (int i = 0; i < N; i++) {
            total += (long long)(h[i] / mid) * (w[i] / mid);
        }
        
        if (total >= K) {
            ans = mid;
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    cout << ans << endl;
    
    return 0;
}
📊 Vector 与数组对比
特性	静态数组	Vector
大小	固定，编译时确定	动态，运行时可变
内存管理	手动	自动
边界检查	无（可能越界）	at()方法有检查
添加元素	需要预知大小	push_back()自动扩展
删除元素	困难	pop_back(), erase()
性能	极快	几乎和数组一样快
灵活性	低	高
内存占用	固定大小	可能略多（预分配容量）

💡 Vector 高级操作
1. 插入和删除
cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5};
    
    // 在指定位置插入
    vec.insert(vec.begin() + 2, 99);  // 在索引2位置插入99: [1,2,99,3,4,5]
    
    // 删除指定位置
    vec.erase(vec.begin() + 3);       // 删除索引3的元素: [1,2,99,4,5]
    
    // 删除指定范围
    vec.erase(vec.begin() + 1, vec.begin() + 3); // 删除索引1-2: [1,4,5]
    
    // 输出
    for (int x : vec) {
        cout << x << " ";
    }
    cout << endl;
    
    return 0;
}
2. 容量操作
cpp
vector<int> vec;
cout << "size: " << vec.size() << ", capacity: " << vec.capacity() << endl;

vec.push_back(1);
cout << "size: " << vec.size() << ", capacity: " << vec.capacity() << endl;

vec.push_back(2);
cout << "size: " << vec.size() << ", capacity: " << vec.capacity() << endl;

vec.push_back(3);
cout << "size: " << vec.size() << ", capacity: " << vec.capacity() << endl;

// 预分配空间（减少重新分配）
vec.reserve(100);  // 预留100个元素的空间
cout << "capacity after reserve: " << vec.capacity() << endl;

// 调整大小
vec.resize(50);    // 调整为50个元素（多余的元素用0填充）
cout << "size after resize: " << vec.size() << endl;
3. 二维 vector
cpp
// 创建二维vector（类似二维数组）
vector<vector<int>> matrix(3, vector<int>(4, 0));  // 3行4列，全为0

// 访问元素
matrix[0][0] = 1;
matrix[1][2] = 5;

// 遍历二维vector
for (int i = 0; i < matrix.size(); i++) {
    for (int j = 0; j < matrix[i].size(); j++) {
        cout << matrix[i][j] << " ";
    }
    cout << endl;
}
🎓 为什么在分巧克力问题中用 vector？
优点
灵活性：N 是输入值，vector 可以根据 N 自动分配空间

安全性：提供边界检查（使用 at()）

方便：可以使用范围 for 循环等现代特性

性能：与静态数组几乎一样快

对比代码
cpp
// 使用静态数组（需要知道最大大小）
int h[100005];  // 浪费空间或不够用
int w[100005];

// 使用vector（精确分配）
vector<int> h(N);  // 刚好N个元素，不多不少
vector<int> w(N);
📝 常用函数速查表
函数	作用	示例
push_back(x)	末尾添加元素	vec.push_back(10);
pop_back()	删除末尾元素	vec.pop_back();
size()	返回元素个数	int n = vec.size();
empty()	判断是否为空	if (vec.empty())
clear()	清空所有元素	vec.clear();
reserve(n)	预留空间	vec.reserve(100);
resize(n)	调整大小	vec.resize(50);
at(i)	访问元素（检查边界）	int x = vec.at(5);
begin()	返回起始迭代器	auto it = vec.begin();
end()	返回结束迭代器	auto it = vec.end();
🎯 总结
Vector 的本质：一个可以自动扩容的动态数组。

何时使用 vector：

✅ 不知道需要多少元素时

✅ 需要动态添加/删除元素时

✅ 希望使用现代C++特性时

✅ 需要STL算法支持时

何时使用静态数组：

✅ 大小固定且已知时

✅ 追求极致性能时

✅ 需要与C代码交互时

在分巧克力问题中，使用 vector 是最佳选择，因为 N 是输入值，我们无法预知大小，vector 可以完美适配！






5. 1 Byte = 8 bits (比特位)

1 KB = 1024 Bytes

1 MB = 1024 KB

1 GB = 1024 MB


6.贪心算法
在一个创意工作室中，三位设计师李工、王工和张工分别负责三项独立的模型制作任务。李工完成任务需要 a1​ 秒，王工需要 a2 秒，张工需要 a3​ 秒。工作室的建模平台一次只能容纳两名设计师工作，第三位设计师需等待，直到平台空闲（即当前一位设计师完成任务离开）才能开始工作。所有模型全部完成时，项目才算正式交付。
现在，经理希望合理调度设计师的工作顺序，以最短时间完成所有任务。请你计算三位设计师完成三件模型的最小总时间。
输入格式
输入仅一行，包含三个正整数a1​,a2​,a3​分别代表三位设计师完成各自任务所需的时间（单位：秒）。
输出格式
输出一个整数，表示完成所有模型的最小总时间（单位：秒）。
样例输入
3 5 7
样例输出
8
#include <iostream>
#include <algorithm>//里面包含max函数
using namespace std;
int main()
{
  int a1,a2,a3,MAX,sum;
  cin >> a1 >> a2 >> a3;
  MAX = max(a1,max(a2,a3));
  sum = a1 + a2 + a3 - MAX;
  cout << (sum>MAX?sum:MAX);
  return 0;
}



7.
<iostream>	cin,cout,cerr,endl 等
<algorithm>	max,min,sort,reverse 等
<cmath>	sqrt,pow,abs等数学函数
<string>	string类型
<vector>	vector容器
<bits/stdc++.h>	所有标准库头文件

