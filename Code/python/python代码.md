## python简洁写法总结

[让你的Python代码更加pythonic](https://wuzhiwei.net/be_pythonic/)

* **字符串反转**
```
s = 'abcdefg'
print(s[::-1])  # gfedcba
“回文串”是一个正读和反读都一样的字符串：input == input[::-1]
```
* **字典的默认值**
```
dic = {'name':'Tim', 'age':23}
dic['workage'] = dic.get('workage',0) + 1
#dic = {'age': 23, 'workage': 1, 'name': 'Tim'}
```
* **for…else…语句**
```
for x in range(1, 5):
    if x == 5:
        print('find 5')
        break
else:
    print('can not find 5!')
# can not find 5!
for...else...的else部分用来处理没有从for循环中断的情况
```
* **zip创建键值对**
```
keys = ['Name', 'Sex', 'Age']
values = ['Tim', 'Male', 23]
dic = dict(zip(keys, values))
# {'Age': 23, 'Name': 'Tim', 'Sex': 'Male'}
```

## python常用函数
1.	enumate( ): 遍历序列中的元素以及他们的下标
```
for index, line in enumerate(inputFile.readlines()):
    if index != 0:
        key = line.strip().split(' ')[0]
        vector = list(line.strip().split(' ')[1:])
```
2.	strip(): 默认删除空白符（包括'\n', '\r',  '\t',  ' ')
```
a = '123abc'
a.strip('21')  <--> a.strip('12') \# 把1和2都删除
```
3.	.format():   "{} {}".format("hello", "world") 格式化输出
```
(‘a’).join(b):  a: 分隔符 b: 需要分隔的数据
b必须为字符串序列 (‘a’, ‘b’, ‘c’), [‘a’, ‘b’, ‘c’]
students={"name1":"joy","name2":"john","name3":"jerry"}   #将key连接起来
>>> jn1.join(students)
'name1-name2-name3'
```
4.	a = [x * x for x in range(1, 11) if x % 2 == 0] # a=[4,16,36,64,100]  list
````
a = [m + n for m in 'ABC' for n in 'XYZ']  # ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
word_idx = dict((c,k+1) for k, c in enumerate(words))
```



