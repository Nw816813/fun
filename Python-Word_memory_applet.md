# Python-Word_Memory_Applet

## 前言

最近在背雅思单词（因为口语太差，先从单词下手），设置的是每日30个单词，原本是用的单词app来进行记忆，
后因最近在看web类的内容，构思自己写一个背单词的网页。设想如下：

1.0.0 将单词存入csv文件，使用pandas读取csv，做一个简单的背单词小程序
2.0.0 使用django与mysql作为程序后台，使用简单的html，来做一个web版本的背单词程序，实现前端录入单词以及检验背单词效果的程序
3.0.0 调用讯飞语音识别api，来实现【听写】功能以及【口语】检验功能
4.0.0 程序迁移为小程序，方便日常脱离电脑使用

叠甲：写这个只是为了练习python的应用以及日常的一个学习，至于其中逻辑跟想法仍有许多不足，大佬愿意指导的话，双手比心送上啦！

1.0.0 版本实现
准备材料：单词以及释义CSV（哈哈哈，第一个单词就是abandon~）

使用工具：
1、random库、pandas库
2、jupyter notebook

# 完整代码：


```python
import random

wrong_words = [] # 用于记录错词的列表
wrong_count = 0 # 用于记录错误的次数
loop_count = 0 # 用于记录循环次数

while loop_count < 30:
    mean = random.choice(words['含义'])
    word = words[words['含义'] == mean]['单词'].tolist()

    print(mean)
    word_Input = input('请输入单词： ')
    if word_Input == word[0]:
        print('拼写成功')
    elif word_Input == 'exit':
        break
    else:
        print('Wrong!!!')
        wrong_words.append(word[0]) # 将错词添加到列表中
        wrong_count += 1 # 错误次数加1

    loop_count += 1 # 循环次数加1

print("结束！共错了{}个单词，错词如下：".format(wrong_count))
for wrong_word in wrong_words:
    print(wrong_word)

```

实现步骤：
1、读取csv文件


```python
# 导入pandas
import pandas as pd

words = pd.read_csv('单词_表格.csv')#读取csv文件，并存储在word中

words # 在jupter中 打印words内容

```

2、读取csv文件


```python
import random # 引入随机库random

while True: # 套用循环
    mean = random.choice(words['含义']) # 将单词释义的内容随机存入变量mean之中
    word = words[ words['含义'] == mean ]['单词'].tolist()# 调取一一对应的单词并转换为列表

    print(mean) # 打印随机的单词释义
    word_Input = input('请输入单词： ') # 设置输入口
    if word_Input == word[0]: # 判断输入单词是否与随机词匹配
        print('拼写成功')
    else:
        print('Wrong!!!')
        break


```

3、设置错词显示以及统计错词数


```python
import random

wrong_words = [] # 用于记录错词的列表
wrong_count = 0 # 用于记录错误的次数
loop_count = 0 # 用于记录循环次数

while loop_count < 30:
    mean = random.choice(words['含义'])
    word = words[words['含义'] == mean]['单词'].tolist()

    print(mean)
    word_Input = input('请输入单词： ')
    if word_Input == word[0]:
        print('拼写成功')
    elif word_Input == 'exit': # 判断退出循环
        break
    else:
        print('Wrong!!!')
        wrong_words.append(word[0]) # 将错词添加到列表中
        wrong_count += 1 # 错误次数加1

    loop_count += 1 # 循环次数加1

print("结束！共错了{}个单词，错词如下：".format(wrong_count))
for wrong_word in wrong_words: # 循环输出错词
    print(wrong_word)

```

程序缺陷：
目前输出的词语存在重复性
没有对数据进行分类，没有根据日期来选择复习单词以及已经学过的、未学习的单词
后续再更新哦~
