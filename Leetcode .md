[TOC]

# LeetCode

## 个人说明

​		从大学毕业开始，总是执着对于工具的掌握，总觉得自己掌握的工具越多，似乎能力就应该强。在慢慢的学习中，对于多种工具的掌握确实在某些知识范围增加了，但是越对工具的掌握，慢慢的感觉到一个感觉：那就是殊途同归，最主要的，还是对问题实际问题的解决，而不管工具怎么变化，总是逃不过实践和理论的学习的结合。

​		回到文中，问什么要开始进行刷题呢？现在已经进行工作了，为什么还要对算法题进行一定。回想了一下，其中的原因也比较复杂，有对自己codeing能力的提高，也有对自己专业知识的增加，也有一定的功利性质。不管怎么说，总是觉得有一些直接的好处。更深层次的原因，或许是想自己的脑子动起来，让自己保持处于一种活动的状态，保持一定的思考能力，也可能是对自己学习的一种锻炼。谁知道呢，总觉得自己的方向是对的。

​		

## 简单题型

### 1.两数之和    ==easy==

$~~~~~~~$个人思路：整体思路难度不大，通过两次遍历，将目标和的索引通过列表的方式返回即可。
遇到问题：1.两次循环中，循环体for中的变量赋值并没有变化，导致在整个思路中解体中出现问题。
解决办法：在for循环体中，由于其循环范围在range中，直接改变range的范围可以改变遍历的范围，完成代码的循环遍历。
		2.语法不熟练：由于熟练度问题，在代码时候存在c语言残留语法思路。通过缩进表现代码逻辑，注意基本语法问题。
个人解题：

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)-1):
            for j in range(i+1,len(nums)):
                if (nums[i]+nums[j]==target):
                    return [i,j]
        return None
```

3.优化思路：
如果不使用两次遍历，是否还有其它相关的接解题方法？从哪里优化？字典会去重，待定。

### 7.整数反转

==easy==
解题思路：1.先判断传如数据是否溢出，溢出直接返回0
2.判断传入数据是正负，如果是负数，按正数处理然后返回值；如果是正数数，将每一位数字取出后，重新填装。
3.再次判断是否溢出。

```python
class Solution:
    def reverse(self, x: int) -> int:
        if((x<-2**31) or ((2**31)-1)<x):
            return 0
        new_num = 0
        cal=x
        if x<0:
            cal =-cal
            while (cal):
                new_num =new_num*10+cal%10
                cal=cal//10
            new_num=-new_num
        else:
            while (cal):
                new_num =new_num*10+cal%10
                cal=cal//10
        if ((new_num < -2 ** 31) or ((2 ** 31) - 1) < new_num):
            return 0
        return new_num
```

优化思路：
待定

### 9.回文数

==easy==
个人思路：分类，负数一定不是回文数；单位数一定是回文数，将数字转化为字符串，通过半数进行遍历，首位相对应的字符不对，则返回Flase，不是回文数。
遇到问题： 在调试时候，对于代码逻辑出现问题，问题出现原因主要是长时间未使用编程语言工具导致。

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x<0:
            return False
        x_str = str(x)
        print(x_str)
        x_str_length=len(x_str)
        if (x_str_length == 1):
            return True

        for i in range(len(x_str)//2):
            print(i)
            print(len(x_str)-1-i)
            if (x_str[i] != x_str[len(x_str)-1-i]):
                return False
        return True
x=121
S1 = Solution()
print(S1.isPalindrome(x))
```

其他解题思路：通过数学方法进行解题，将数字倒过来，与原数字尽心对比，自我实现思路比较乱，看起来杂乱无章，没有深刻的理解其本质。

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        new_num = 0
        cal=x
        if x<0:
            return False
        while (cal/10):
            x1=cal%10
            print(x1)
            new_num =(new_num+x1)*10
            cal=cal//10
        new_num=new_num//10
        print(new_num)
        return x==new_num

x=111
S1 = Solution()
print(S1.isPalindrome(x))
```

```python
#简化代码：
class Solution:
    def isPalindrome(self, x: int) -> bool:
        new_num = 0
        cal=x
        if x<0:
            return False
        while (cal):
            new_num =new_num*10+cal%10
            cal=cal//10
        return x==new_num
```

### 13.罗马数字转整数

==easy==

在整个逻辑中，除了罗马数字几个原始的情况，看起来逻辑比较复杂。

错误代码：错误原因，由于规则问题，罗马数字左边大，右边小，而其==特殊字符字典可能出现在字符的各个位置==；测试用例通过率：2193/3999

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        romanDic ={'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        romanSpecDic ={'IV':4,'IX':9,'XL':40,'XC':90,'CD':400,'CM':900}
        str_length =len(s)
        for i in range(str_length):
            if(s[i] not in romanDic):
                return False
        if(1==str_length):
            return romanDic[s]

        romanToInt = 0
        if(s[0:2] in romanSpecDic):
            for i in range(2,str_length):
                romanToInt=romanDic[s[i]]+romanToInt
            return romanToInt+romanSpecDic[s[0:2]]
        else:
            for i in range(str_length):
                romanToInt=romanDic[s[i]]+romanToInt
        return romanToInt

x='MCMXCIV'

S1 = Solution()
print(S1.romanToInt(x))
```

错误代码块2：错误原因：python语法问题，python语法中， ==for循环中的迭代器不能够随意改变==。暂时替代方法只能够是使用while进行改写

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        romanDic ={'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        romanSpecDic ={'IV':4,'IX':9,'XL':40,'XC':90,'CD':400,'CM':900}
        str_length =len(s)
        for i in range(str_length):
            if(s[i] not in romanDic):
                return False
        if(1==str_length):
            return romanDic[s]

        romanToInt = 0
        for i in range(str_length-1):
            if (s[i:i+2] not in romanSpecDic):
                romanToInt =romanDic[s[i]]+romanToInt
            else:
                romanToInt = romanToInt+romanSpecDic[s[i:i+2]]
                i = i+2
            print(romanToInt)
        return romanToInt

x='MCMXCIV'
#1994
print(x[1:2])

S1 = Solution()
print(S1.romanToInt(x))
```

通过代码：

```python
     class Solution:
    def romanToInt(self, s: str) -> int:
        romanDic ={'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        romanSpecDic ={'IV':4,'IX':9,'XL':40,'XC':90,'CD':400,'CM':900}
        str_length =len(s)
        if (1 == str_length):
            return romanDic[s]
        i = 0
        romanToInt = 0
        while i<str_length:
            if(s[i] not in romanDic):
                return False

            if (s[i:i+2] not in romanSpecDic):
                romanToInt =romanDic[s[i]]+romanToInt
                i=i+1
            else:
                romanToInt = romanToInt+romanSpecDic[s[i:i+2]]
                i = i+2
            print(romanToInt)
        return romanToInt

x='MCMXCIV'
#1994
print(x[1:2])

S1 = Solution()
print(S1.romanToInt(x))
```

优化空间：//待定,部分语句优化。



### 14.最长公共子串   //优化

==easy==
解决问题：将一个列表中的字符串，所有字符串的最大公共子串输出，如果没有，返回为空。
条件：每个字符串最大为200个，每个字符串仅有英文字母组成。
个人思路：1.先看是否有一个字符串为空，如果为空，先返回空，如果全不为空，进行下一步判断。
2.如何寻找字符串最长的公共前缀？如果每个字符串进行单独遍历，那么整个算法的复杂度相当的大。列表的字符串个数未知。
整体思路，遍历一次字符列表，只找相邻两个字符串的子字符串，在找到子相邻两个的子串再到第三个字符串进行对比，如果第三个字符串存在，则继续遍历，在遍历过程中，如果发现该字符串有多余，则减少子串长度。其中值要求查找最长==前缀==
错误代码快：
错误原因：python循环体中的变量操作问题，以及其变量在循环体中的作用域问题相关，导致代码调试出现问题。
测试用例通过112/123

```python
class Solution:
    def longestCommonPrefix(self, strs:'List[str]') -> str:

        if (1==len(strs)):
            return strs[0]
        for i in strs:
            if(i==''):
                return ''
        j=0
        subStrs=''
        subL=[]
        for i in range(len(strs)-1):
            j=0
            subStrs=''
            while j<min(len(strs[i]),len(strs[i+1])):
                if(strs[i][j]==strs[i+1][j]):
                    subStrs=subStrs+(strs[i][j])
                    j=j+1
                else:
                    j=0
                    break
            subL.append(subStrs)
            print(subL)
        return subStrs


strs = ["flower","flow","flight","flower"]
S1 =Solution()
print(S1.longestCommonPrefix(strs))
```



错误代码：
调试错误代码几个重要的总结：1.在进行列表等循环的时候，最好避免使用for循环，for循环在运行时候的中间体结构变量会出现会带来不必要的复杂。
2.注意审题，对题目的清晰理解，最开始由于题目的阅读不清晰导致浪费了大量时间。
3.变量相关问题：对于整体思路和逻辑需要进行有理有根据，想好了再动手，对于变量的命名，尽量规范，并且尽量看命知道含义。
4.在进行解题逻辑的时候，思路的整体把握要高于整体乱敲代码的状况。
5.待定

```python

class Solution:
    def longestCommonPrefix(self, strs: 'List[str]') -> str:

        if (1 == len(strs)):
            return strs[0]
        for i in strs:
            if (i == ''):
                return ''
        j = 0
        subStrs = ''
        subL = []
        for i in range(len(strs) - 1):
            j = 0
            subStrs = ''
            while j < min(len(strs[i]), len(strs[i + 1])):
                if (strs[i][j] == strs[i + 1][j]):
                    subStrs = subStrs + (strs[i][j])
                    j = j + 1
                else:

                    break

        return subStrs


strs = ["flower", "flow", "flight"]
S1 = Solution()
print(S1.longestCommonPrefix(strs))
```

正确提交代码：

```python
class Solution:
    def longestCommonPrefix(self, strs: 'List[str]') -> str:

        if (1 == len(strs)):
            return strs[0]
        for i in strs:
            if (i == ''):
                return ''
        i=0
        j = 0
        subStrs = ''
        subL = []
        for i in range(len(strs)-1):
            j = 0
            subStrs = ''
            while j < min(len(strs[i]), len(strs[i + 1])):
                if (strs[i][j] == strs[i + 1][j]):
                    subStrs = subStrs + (strs[i][j])
                    j = j + 1
                else:
                    break
            subL.append(subStrs)
       # print(subL)
        k = 0
        m=len(subL[0])
        sublIndex=0
        while k<(len(subL)):
            #print(k)
            if (subL[k] == ''):
                return ''
            elif (1==len(subL[k])):
                sublIndex=k
            else:
                if(len(subL[k])<=m):
                    m=len(subL[k])
                    sublIndex=k
            k=k+1
        #print(f'm is {sublIndex}')
        return subL[sublIndex]
```

3.优化路径
本次代码再空间上可以进行优化。在寻找到相邻两个字符的字串的时候，可以减少一个LIST的消耗，以及相关局部变量的使用，局部变量的使用的时候，其许中间变量可以尽量省去。
其他方法相关解答：//待定

解决方法优化：//待定

### 20.有效括号

==easy==

解决问题：判断字符串是否有效，括号必须闭合顺序闭合。==栈相关，待定==
个人思路：两天无思路，难度较大，需要进行改进，看时候有其他方法。

在解决本体的过程中，有一点思路：
1.先把各种出现的问题都考虑到各种情况的问题，相当于测试用例
2.如果在两个小时内找不到思路，直接看解析解答题目。
3.注意代码边界问题，就是执行的列表，字典等边界，元素问题。
4.从学习到模仿。

```python
class Solution:
    def isValid(self, s: str) -> bool:
        strDic={'(':')','[':']','{':'}','？':'？'}
        if(len(s)%2!=0):
            return False
        if(s[0]==')' or s[0]==']' or s[0]=='}'):
            return False
        strStack = ['？']
        for ch in s:
            if ch in strDic:
                strStack.append(ch)
            elif(strDic[strStack.pop()]!=ch):
                return False
        return len(strStack)==1

strs = '"(){}}{"'
S1 = Solution()
print(S1.isValid(strs))
```

重构代码：该思路来源于官方解题：该方法巧妙的解决了空栈的相关问题

```python
class Solution1:
    def isValid(self, s: str) -> bool:
        strDic={')':'(',']':'[','}':'{',}
        if(len(s)%2==1):
            return False
        strStack = []
        for ch in s:
            if ch in strDic:
                if(not strStack or strStack[-1]!=strDic[ch]):
                    return False
                strStack.pop()
            else:
                strStack.append(ch)
        return not strStack
```

另一种方法：可以测试：
将（），{}，[],这种可以闭合的括号直接都替代成’‘，然后计算s的长度。
代码展示：

### 21.合并两个链表

//待定,该链表是类实现，但是该值不好模拟。递归思想



### 26.删除有序数组中的重复项

删除数组中的重复元素，一个元素只留一个，并返回其新长度，算法要求的复杂度O（1）。

个人思路：由于列表是有序的，直接判断相邻两个数值的变化，变化次数+1则为该所有的长度，通过长度下标，将值从新填充到nums，返回该列表的长度即刻。

```python
class Solution:
    def removeDuplicates(self, nums: 'List[int]') -> int:
        i = 1
        diffNum = 0
        if(len(nums)==1):
            return 1
        else:
            while i<len(nums):
                if nums[i]!=nums[i-1]:
                    diffNum=diffNum+1
                    nums[diffNum]=nums[i]
                i=i+1
        
        return diffNum+1
L1=[0,0,1,1,1,1]
S1 = Solution()
print(S1.removeDuplicates(L1))
```

优化思路：如何将一个元素的时候合并到一个循环中去？基本上是不用处理，著需要处理为空的列表情况。

```python
class Solution:
    def removeDuplicates(self, nums: 'List[int]') -> int:
        i = 1
        diffNum = 0
        if(len(nums)==0):
            return 0
        else:
            while i<len(nums):
                if nums[i]!=nums[i-1]:
                    diffNum=diffNum+1
                    nums[diffNum]=nums[i]
                i=i+1
        print(nums[:diffNum+1])
        return diffNum+1

L1=[0]
S1 = Solution()
print(S1.removeDuplicates(L1))
```

### 27.移除元素

原地移除数值中等于val的值，其复杂度为O(1)，==元素顺序可以改变==，
个人思路：遍历一边该列表，经值等于val的与列表交换。最后返回列表个数数量值
该代码通过测试用例：85/113

```python
class Solution:
    def removeElement(self, nums: 'List[int]', val: int) -> int:
        n= len(nums)
       
    
        while i<j:
            if nums[j]==val:
                j=j-1
            if nums[i]==val:
                tempvar=nums[j]
                nums[j]=nums[i]
                nums[i]=tempvar
            i=i+1
        print(nums)
        return j+1

L1=[3]
S1 = Solution()
print(S1.removeElement(L1,3))
#本代码不能解决列表数量为1，或者数量>2的相同元素的情况。看看是否能够改进。
```

不通过情况：元素数值为1个，然后其val也是为1的情况。
问题：使用双指针式没问题，但是解题思路出现问题。由于不需要值的顺序，可以直接将不对的值覆盖掉，不需要交换，也可以实现其效果。

```python
class Solution:
    def removeElement(self, nums: 'List[int]', val: int) -> int:
        n= len(nums)
        i =0
        j=0
        while i<n:
            if nums[i]!=val:
                nums[j]=nums[i]
                j=j+1
            i=i+1
        print(nums)
        return j
```





### 33.搜索旋转排序数组

由于将有序数组旋转后，分成两部分，其中有部分
个人思路：直接遍历，可以通过，但是本题目的考点并不在该方面
个人代码：

```python
class Solution:
    def search(self, nums: 'List[int]', target: int) -> int:
        i=0
        index =0
        while(i<len(nums)):
            if(nums[i]==target):
                return i

            i=i+1
        return -1
```

优化代码：//待定

将数组一分为二，其中一定有一个是有序的，另一个可能是有序，也能是部分有序。此时有序部分用二分法查找。无序部分再一分为二，其中一个一定有序，另一个可能有序，可能无序。就这样循环. 

```python
class Solution:
    def search(self, nums: 'List[int]', target: int) -> int:
        if not nums:
            return -1
        Lindex=0
        Rindex= len(nums)-1
        while(Lindex<=Rindex):
            Mindex = Lindex+(Rindex-Lindex)//2
            if(nums[Mindex]==target):
                return Mindex
            if(nums[0]<=nums[Mindex]): #有序部分，一直有序
                if(nums[0]<=target<nums[Mindex]):
                    Rindex = Mindex-1
                else:
                    Lindex = Mindex+1
            else:  #有序部分+无序部分
                if(nums[Mindex]<target<=nums[len(nums)-1]):
                    Lindex = Mindex + 1
                else:
                    Rindex = Mindex - 1
        return -1
```

### 35.搜索插入位置

题目意图：使用log（n）算法查找一个有序的列表，如果查找到该值，就返回其索引，如果没有查找到，则返回该插入的下标：

解题思路：根据算法复杂度，该题必然是使用二分查找，然后是否可以根据二分查找改进，使得该题完成提示。

二分查找代码：

```python
class Solution:
    def searchInsert(self, nums: 'List[int]', target: int) -> int:
        LIndex =0
        RIndex =len(nums)-1

        while(nums[midIndex]!=target):
            midIndex = LIndex + (RIndex - LIndex) //2
            if(nums[midIndex]==target):
               return midIndex

            if(nums[midIndex]<target):
                LIndex=midIndex+1
            else:
                RIndex = midIndex-1
L1=[0,1,3,5,6,8,9,11]
S1 = Solution()
print(S1.searchInsert(L1,0))
```

那如何改进二分查找，将该插入地方的值的index返回呢？

```python
class Solution:
    def searchInsert(self, nums: 'List[int]', target: int) -> int:
        LIndex =0
        RIndex =len(nums)-1

        midIndex = LIndex + (RIndex - LIndex) // 2
        while(LIndex<=RIndex):
            midIndex = LIndex + (RIndex - LIndex) //2
            if(nums[midIndex]==target):
               return midIndex

            if(nums[midIndex]<target):
                LIndex=midIndex+1
            else:
                RIndex = midIndex-1
        return LIndex

L1=[0,1,3,5,6,8,9,11]
S1 = Solution()
print(S1.searchInsert(L1,8))
```

q：为什么插入索引的位置就是RIndex？
根据if的判断条件，left左边的值一直保持小于target，right右边的值一直保持大于等于target，而且left最终一定等于right+1，这么一来，循环结束后，在left和right之间画一条竖线，恰好可以把数组分为两部分：left左边的部分和right右边的部分，而且left左边的部分全部小于target，并以right结尾；right右边的部分全部大于等于target，并以left为首。所以最终答案一定在left的位置。

### 53.最大子序和  ==未解决==   分治，dp

题目意图：意思是在一个列表中，找出里面的子列表和最大的值，不需要返回index。

解题思路：总体难度比较大，个人思路是将每个子序列的和算出来，找出最大的值，该算法复杂度较高，对于题目进行源码查看后，发现该源码难度还是相当的大，该题可以使用动态规划，分治等思想都可以解题，对于思路的启发很有帮助，所以都将该题作为案例进行学习。

### 748 最短补全词

这题为简单，但是硬是给刚出来了，在算法的实践层面上面讲是失败的，但是还是做出来，做出来的意义就是可以知道自己的水平较差，还有很多可以优化的地方，之前不相信有人用很低的实践复杂度和空间复杂度做出来了，现在知道确实存在，所以每个块都有每个块的技巧,需要进一步提高

```python
class Solution:
    def shortestCompletingWord(self, licensePlate: str, words: 'List[str]') -> str:

        licensePlate = licensePlate.lower()   #不区分大小写，转化为小写
        licensePlateList = []
        for str in licensePlate:
            if str.isalpha():
                licensePlateList.append(str)   #将字符提出来

        for i in range(len(words)):
            words[i] = words[i].lower()   #不区分大小写，转化为小写处理。

        #统计licensePlateList中的元素
        licensePlateDic ={}
        for i in licensePlateList:
            if licensePlateList.count(i)>0:
                licensePlateDic[i]=licensePlateList.count(i)
        print(licensePlateDic)
        KeyList=[]
        for key  in licensePlateDic.keys():
            KeyList.append(key)

        KeyN=len(KeyList)
        print(KeyN)

        wordsN =len(words)
        wordsDic =[{} for i in range(0,wordsN)]
        print(wordsDic)
        for i in  range(0,wordsN):
            for j in range(0,KeyN,1):
                wordsDic[i][KeyList[j]]=words[i].count(KeyList[j])

        print(KeyList)
        print(wordsDic)
        #存在问题，并没有将有效word提出来
        wordsFlist =[]
        keyCount =0
        for i in range(wordsN):
            for j in KeyList:
                if wordsDic[i][j]>=licensePlateDic[j]:
                    keyCount= keyCount+1
                    if keyCount ==KeyN:
                        wordsFlist.append(words[i])
                        keyCount = 0
                else:
                    keyCount = 0    ##如果不添加等于0，bug出现 keyCount在两个数量为1的情况下会出现异常值
                    break

        print(wordsFlist)
        print('#########wordFlist###############')

        FIndex = 0                         #在筛选的结果中找最小字母，或者最靠前的结果
        wordsFlist_N = len(wordsFlist)
        wordsMinL= len(wordsFlist[0])
        for i in range(0,wordsFlist_N,1):
           if len(wordsFlist[i])<wordsMinL:
                wordsMinL =len(wordsFlist[i])
                FIndex = i
        print(wordsFlist[FIndex])
        return wordsFlist[FIndex]

licensePlate = "1s3 456"
words = ["looks", "pest", "stew", "show"]

s = Solution()
print(s.shortestCompletingWord(licensePlate,words))

```



## 线性表

### 数组

Remove Duplicates from Sorted Array （移除有序数组中的重复元素）

#### 题号：26  移除有序数组中的重复元素； 难度：简单    
题目：有序数组，原地删除重复出现的元素，使得每个元素只出现一次，返回删除后数组的新长度。
要求复杂度为O(1)
思路： 条件：有序数组。使用两个索引i，j，判断当前所在索引和后面索引的值是否相等，如果相同，则继续移动索引j，直到i，j值不相等，则交换两个值。

```python
class Solution:
    def removeDuplicates(self, nums: 'List[int]') -> int:
        i = 1
        diffNum = 0
        if(len(nums)==1):
            return 1
        else:
            while i<len(nums):
                if nums[i]!=nums[i-1]:
                    diffNum=diffNum+1
                    nums[diffNum]=nums[i]
                i=i+1
        print(nums[:diffNum+1])
        return diffNum+1
```



Remove Duplicates from Sorted Array （移除有序数组中的重复元素）
#### 题号：80 移除有序数组中的重复元素 ； 难度：==中等==
思路：做过相似的题目，思路是对的，但是写不出来代码。
参考算法：
		使用两个指针，左指针和右指针，其中右指针始终往后移动。由于单个元素最多只能出现两次，所以只需要判断right和left-2的值是否相同如果相同:右指针继续往后移动，左指针不动；如果不相同，右指针指向的值要覆盖掉左指针的值，然后左指针后移一步。

```python
class Solution:
    def removeDuplicates(self, nums: 'List[int]') -> int:

        numsLenght = len(nums)
        if numsLenght<2:
            return numsLenght
        
        i = 2
        j = 2

        while(j<numsLenght):
            if nums[j]==nums[i-2]:
                j = j+1
            else:
                nums[i] =nums[j]
                j=j+1
                i=i+1
        return i
```

如果将代码换成for循环：

```python
class Solution:
    def removeDuplicates(self, nums: 'List[int]') -> int:
        u = 0
        k = 2  #可以将k递推到连续k个数字进行
        for i in nums:
            if(u<2 or nums[u-k]!=i):
                nums[u] = nums[i]
                u=u+1
        return u
```

#### 题号：33  搜索旋转排序数组； 难度：==中等==

 搜索旋转排序数组（Search in Rotated Sorted Array）
题目：将一个有序的数组按升序排列，其中数组中的值不同，旋转后找出该值。
解题思路：该数组之前有序，由于旋转后，变得部分有序，部分无需，可以使用二分法，进行搜索，该题为二分法的变种题目。
该题不用考虑边界问题
1.使用二分搜索时，会将数组分为两半。分开讨论。
2.对比序列首元素和mid值的大小，如果mid值大于首元素，则其中为有序的，使用二分查找；
2.在mid和尾部元素间，分为有序或者无序的情况，然后进行二分查找。

```python
class Solution:
    def search(self, nums: 'List[int]', target: int) -> int:
        numsLength = len(nums)
        if numsLength==0:
            return -1
        left = 0
        mid =0
        right =numsLength-1
        while left<=right:
            mid = left+(right-left)//2
            if nums[mid]==target:
            	return mid
            if nums[0]<=nums[mid]:
                if(nums[0]<=target<nums[mid]):  #左边有序，值在左边，并在左边二分查找
                    if nums[mid]>target:
                        right =mid-1
                    else:
                        left = mid+1
                else:
                    left = mid+1   #值不在左边，准备在右边查找
            else:
                if nums[mid]<target<=nums[numsLength-1]: #右边有序，值在右边，并二分查找
                    if nums[mid] > target:
                        right = mid - 1
                    else:
                        left = mid + 1
                else:
                    right = mid-1 #值不在右边，准备在左边查找。
        return -1
```

该代码可以简化，在目标值在所选区域内是，可以对逻辑进行简化。

```python
class Solution:
    def search(self, nums: 'List[int]', target: int) -> int:
        if not nums:
            reurn -1
        Lindex=0
        Rindex= len(nums)-1
        while(Lindex<=Rindex):
            Mindex = Lindex+(Rindex-Lindex)//2
            if(nums[Mindex]==target):
                return Mindex
            if(nums[0]<=nums[Mindex]): #有序部分，一直有序
                if(nums[0]<=target<nums[Mindex]):
                    Rindex = Mindex-1
                else:
                    Lindex = Mindex+1
            else:  #有序部分+无序部分
                if(nums[Mindex]<target<=nums[len(nums)-1]):
                    Lindex = Mindex + 1
                else:
                    Rindex = Mindex - 1
        return -1
```

改进版本：这样将界限缩小，使得二分查找更加容易理解：

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1
        l, r = 0, len(nums) - 1
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] == target:
                return mid
            if nums[l] <= nums[mid]: #将nums[0] 替换成nums[l]
                if nums[l] <= target < nums[mid]:
                    r = mid - 1
                else:
                    l = mid + 1
            else:
                if nums[mid] < target <= nums[r]: ##将nums[len(nums-1)] 替换成nums[r]
                    l = mid + 1
                else:
                    r = mid - 1
        return -1

```

#### 题号：81 搜索旋转排序数组2 ； 难度：==中等==
搜索旋转排序数组2（Search in Rotated Sorted Array I I）
题意; 与旋转数组相似，条件不同：主要由不同是数组中存在相同元素。数组以某个元素旋转了。

问题：重复元素对算法排序有什么影响？
标准二分搜索时可以使用在有序重发的元组中，因此，本题目的主要问题在于由于有重复元素，无法分开那一部分有序，那一部的数组时无序，这个问题。

```python
#标准二分搜索，可以搜索有序重复数组的元素，但是搜索效率会受到影响。
def binary_search(arr: list, e: int) -> int:
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if e == arr[mid]:
            return mid
        elif e < arr[mid]:
            right = mid - 1
        else:
            left = mid + 1
    return -1

```

结题代码：旋转数组的改进二分需要找判断那部分时有序的，(left,mid)和（r，mid）的哪部分有序列，然后使用题33的算法即可

```python
class Solution:
    def search(self, nums: 'List[int]', target: int) -> int:
        numsLength = len(nums)
        if numsLength == 0:
            return False
        if numsLength==1:
            return nums[0]==target
        left = 0
        mid = 0
        right = numsLength - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return True
            if nums[left] == nums[mid] and nums[mid] == nums[right]:#由于时重复元素，找不到分界点
                left += 1
                right -= 1
            elif nums[left] <= nums[mid]:
                if (nums[left] <= target < nums[mid]): 
                    if nums[mid] > target:
                        right = mid - 1
                    else:
                        left = mid + 1
                else:
                    left = mid + 1  
            else:
                if nums[mid] < target <= nums[right]: 
                    if nums[mid] > target:
                        right = mid - 1
                    else:
                        left = mid + 1
                else:
                    right = mid - 1  
        return False
```



#### 题号：4  两个有序数组的中位数； 难度：==hard==        //待优化              

==第一个hard题==

两个有序数组的中位数（Median of Two Sorted Arrays）
题意; 给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。算法的时间复杂度应该为 O(log (m+n)) 。
思路：实现难度不大，但是需要将算法复杂度控制在O(log (m+n))，没有思路，先对数组进行常规解题，看看是否能够通过。
实际可以通过，但是使用时间和内存消耗比较低，能够完成基本功能。

```python
class Solution:
    def findMedianSortedArrays(self,nums1, nums2) :
        #分为奇数和偶数，奇数为最中间的值，偶数为中间两个数的和的均值。
        #算法要求复杂度：log（m+n）
        for i in nums2:
            nums1.append(i)
        nums1.sort()    #排序算法可以如果使用快排，希尔之类的，时间复杂度将会提高到nlog(n).似乎无法优化。
        n1 = len(nums1)
        if(n1<2):
            return nums1[0]
        elif (n1)%2==1:
            return nums1[n1//2]
        else:
            return (nums1[n1//2]+nums1[n1//2-1])/2
```

如何优化？
官方方法：两种方法
1.使用归并的方式，合并两个有序数组，得到一个大的有序数组。大的有序数组的中间位置的元素，即为中位数。
算法复杂度，和空间复杂度：O(m+n)
2.不需要合并两个有序数组，只要找到中位数的位置即可。由于两个数组的长度已知，因此中位数对应的两个数组的下标之和也是已知的。维护两个指针，初始时分别指向两个数组的下标 00 的位置，每次将指向较小值的指针后移一位（如果一个指针已经到达数组末尾，则只需要移动另一个数组的指针），直到到达中位数的位置。
空间复杂度降到 O(1)，但是时间复杂度仍是 O(m+n)。

对归并排序进行了一次书写，但是问题很大。整体思路没问题，处了问题。

```python
def mergeSort(nums):
    print(nums)
    if len(nums)>1:    #作用域问题：如果将下面两个while语句中的变量是否能够使用的问题。如果将变变量定义在if中而if并没有生效，则会报错：UnboundLocalError: local variable 'xxx' referenced before assignment。但是在函数内部，python没有作用域的概念，python中，模块，函数，类范围和命明空间有作用域限定。
        mid = len(nums) // 2
        lefthalf=nums[:mid]#切片的区间：前闭后开
        righthalf =nums[mid:]
        mergeSort(lefthalf)
        mergeSort(righthalf)

        i = 0
        j = 0
        k = 0
        while (i<len(lefthalf) and j<len(righthalf)):#算法本身问题：在归并的时候，是需要额外分配内存空间。
            if lefthalf[i]<righthalf[j]:
                nums[k] = lefthalf[i]
                i = i+1
            else:
                nums[k] = righthalf[j]
                j = j+1
            k =k+1
        while(i<len(lefthalf)):
            nums[k] = lefthalf[i]
            i=i+1
            k = k+1
        while (j < len(righthalf)):
            nums[k] = righthalf[j]
            j = j + 1
            k = k + 1

nums= [54,26,93,17,77,31,44,55,20]
mergeSort(nums)
print(nums)

```

归并==思考==：那么如果要考虑将归并排序转化为非递归的形式，这个问题如何处理？在处理该问题的时候，必然会使用到循环，如何结合循环将归并结合起来?

​		本题使用归并的算法基本无法满足O（log（m+n））的算法特征，由于该题达到log（m+n）一般使用的是二分法。数组的数量是m+n，如果数量是奇数，函数返回值为（m+n）//2。如果是偶数，则为第 (m+n)//2个元素和第 (m+n)//2+1个元素的平均值

优化：==待定== 难度较大

#### 题号：128 最长连续数列； 难度：==中等==
最长连续数列（Longest  Consecutive Sequence）
题意：一个无序的数组，找出连续的最长序列的最长长度。不要求数组的位置连续。要求算法复杂度为O(n)
test case：输入：nums = [100,4,200,1,3,2] ：输出为4，==可以存在重复元素==

先按个人解题思路来，排序，然后设置计数器，计数，返回最大的连续的个数。改解题思路在时间复杂度上不占优。

```python
class Solution:
    def longestConsecutive(self, nums:'List[int]') -> int:
        if not nums:
            return 0

        nums.sort()  #排序问题，优化大师点，如何在不使用排序的情况下，将问题解决。
        print(nums)
        conConter = 1
        conConterMax =1

        i = 0
        while i<(len(nums)-1):
            if (nums[i+1]-nums[i] )==1:
                conConter = conConter+1
                conConterMax =max(conConter,conConterMax) #max基本不消耗算法的复杂度。
            elif((nums[i+1]-nums[i])==0): #消除重复元素的影响。如果无该步骤，测试用例一半无法通过。
                conConter = conConter
            else:
                conConter=1
            i=i+1
        return conConterMax
```

官方解题中，使用了hash表或者集合的方式去重，然后使用集合语法进行判断，并没有排序，使得。方法非常巧妙。

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        longest_streak = 0
        num_set = set(nums)

        for num in num_set:
            if num - 1 not in num_set: #寻找小值，有比当前num小的跳到下个循环。没有就执行循环搜索，直接找current_steak。
                current_num = num
                current_streak = 1

                while current_num + 1 in num_set:
                    current_num += 1
                    current_streak += 1

                longest_streak = max(longest_streak, current_streak)#保存每轮的最大的streak。

        return longest_streak
```

#### 题号：1  两数之和（two sum）； 难度：简单
两数之和（two sum）
题意：在一个数组中，找到和为target的两个整数。并返回他们的下标。
官方解答是使用字典的方式，比较巧妙的使用了字典的方式，以及enumerate进行索创建解题。

```python
class Solution:
    def twoSum(self, nums, target) :
        hashtable = dict()  #创建空字典
        for i, num in enumerate(nums):  #将nums生成为索引和元素的元组。（索引，元素） 并避免了两个相同元素被字典删除的情况。
            if target - num in hashtable:
                return [hashtable[target - num], i]
            hashtable[nums[i]] = i # 字典存放内容：（值，索引）
        return []

nums = [2,7,11,15]
target = 9
s = Solution()
print(s.twoSum(nums,target))
```

知识点：

```python
#enumerate(nums)使用
hashtable1 = dict()
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print(list(enumerate(seasons)))  #将nums生成为索引和元素的元组。然后被转为列表
#[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
for i, num in enumerate(seasons):
    print(f'first is {i}, and the second is {num}')
```



#### 题号：15 三数之和（3sum）； 难度：==中等==
三数之和（3sum）
题意：包含n个元素的数组，如果三个元素a，b，c相加的值为0，返回所有和为0不重复的三元组。
个人想法：无任何想法和思路。本题的难度偏高，个人能力思考出来有难度。
官方思路：该题主要是一个双指针相关的题目，如果只用暴力解决方法，其算法的复杂度在O（n**3），并且还要对其进行去重。如果使用双指针的方法的话，可以将算法复杂度控制在哦O（n2）。整体的算法流程：选取第一

```python
class Solution:
    def threeSum(self, nums:'List[int]'):
        nums.sort()
        print(nums)
        n = len(nums)
        ans = list()

        for first in range(n):
            if first>0 and nums[first] ==nums[first-1]: #保证与上次出现的first不同。处理的是不同的值
                continue       #跳出本层循环，继续循环
            print(nums[first])
            third = n-1
            target = -nums[first]
            for second in range(first+1,n):
                if second>first+1 and nums[second] == nums[second-1]:#不会越界，数组范围
                    continue
                while second<third and nums[second]+nums[third]>target :  #同样的去重操作。
                        third = third -1
                if second == third:
                    break    #终止循环
                if nums[second]+nums[third] ==target:
                    ans.append([nums[first],nums[second],nums[third]])
        return ans

```



#### 题号：16 最近三数之和（3Sum Closest）； 难度：==中等==
最近三数之和（3Sum Closest）
题意，一个数组中，找三个数的和，使得三个数的和与目标值target的值最接近。
个人思路：暴力搜索肯定是能够解决的，算法复杂度O（n3），尝试的写写看，然后思考优化版本.测试用例中，通过40个，由于其中算法复杂度已经超时了，解题方面，技巧不成熟，暴力破解无法通过部分结果。算法本身层面可以运行，但是存在一定的问题。

```python
class Solution:
    def threeSumClosest(self, nums: 'List[int]', target: int) -> int:
        #题目假设值存在一组解
        n = len(nums)
        nearlySum =[]
        nearlyAbs = []
        for i in range(0,n):# 为什么不限制迭代器也不会溢出，待定，如果不写成限制状态，也不会报错
            for j in range(i+1,n):
                for k in range(j+1,n):
                    #print(f'the i is {i}, j is {j}, k is {k}')
                    nearlySum.append(nums[i]+nums[j]+nums[k])
                    nearlyAbs.append(abs(nums[i] + nums[j] + nums[k]- target))
        print(nearlySum)
        print(nearlyAbs)
        print(min(nearlyAbs))
        for i in range(0,len(nearlyAbs)):
            if nearlyAbs[i] ==min(nearlyAbs):
                return nearlySum[i]
        return None

nums = [13,2,0,-14,-16,2]
target =-59
s1 =Solution()
print(s1.threeSumClosest(nums,target))

```

官方优化：官方思路太乱，不一定作为参考的答案。思路主要还是排序后，使用双指针，在排序的时候，有写bug，并在查找的时候未查找到。

```python
class Solution:
    def threeSumClosest(self, nums: 'List[int]', target: int) -> int:
        nums.sort()
        print(nums)
        n= len(nums)
        sumFal = nums[0] + nums[1] + nums[n-1]
        AbsMIn = abs(nums[0] + nums[1] + nums[n-1]-target)
        for i in range(0,n):
            leftIndex = i + 1
            rightIndex = n - 1
            while(leftIndex<rightIndex):
                sum = nums[i] + nums[leftIndex] + nums[rightIndex]
                if AbsMIn>abs(sum-target): #在对比绝对值大小的时候，要对每次的绝对值进行缓存，然后对sum的值进行保存
                    AbsMIn = abs(sum-target)
                    sumFal =sum
                if(sum>target):
                    rightIndex = rightIndex-1
                elif(sum<target):
                    leftIndex= leftIndex+1
                else:
                    return target
        return sumFal
```



#### 题号：31，下一个排列（Next Permutation)； 难度：==中等==

下一个排列（Next Permutation)
题意：未看懂题目，好像是排序相关。
解析：给定数字序列的字典序中下一个更大的排列，如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。eg：123<132<312<321
主要解析：需要找一个比当前数大，只需要将后面的大数与前面的小数交换，另外增加的幅度要尽可能小。
满足增加的幅度尽可能小：需要从右边往左边找，然后尽可能用小的大数去与前面的小数交换，将大叔交换到前面后，需要将大数后面的序列重置为升序，升序就是最小的排列。

以 123465 为例：首先按照上一步，交换 5 和 4，得到 123564；然后需要将 5 之后的数重置为升序，得到 123546。显然 123546 比 123564 更小，123546 就是 123465 的下一个排列

算法过程  ==为什么要这么做？==
标准的“下一个排列”算法可以描述为：
1.从后向前查找第一个相邻升序的元素对 (i,j)，满足 A[i] < A[j]。此时 [j,end) 必然是降序（j=i+1）
2.在 [j,end) 从后向前查找第一个满足 A[i] < A[k] 的 k。A[i]、A[k] 分别就是上文所说的「小数」、「大数」
3.将 A[i] 与 A[k] 交换
4.可以断定这时 [j,end) 必然是降序，逆置 [j,end)，使其升序
5.如果在步骤 1 找不到符合的相邻元素对，说明当前 [begin,end) 为一个降序顺序，则直接跳到步骤 4



通过参考和自己写的代码，在测试用例中，通过212/265,为能通过的测试用例为[1,5,1]，通过调试器检测问题

```python
class Solution:
    def nextPermutation(self, nums: 'List[int]') -> None:
        n=len(nums)
        i = n-2
        while i>=0 and nums[i]>nums[i+1]:
            i= i-1
        print(f'nums[i] {nums[i]}')

        j = n-1
        while j>0 and nums[i]>=nums[j]: #添加等号测试用例通过为228，但是为逆序的数字还是未处理。
            j = j-1
            print(f'nums[j] {nums[j]}')
        nums[j],nums[i]=nums[i],nums[j]

        left = i+1
        right= n-1
        while left<=right:
            nums[right],nums[left]=nums[left],nums[right]
            left = left+1
            right = right-1
```

```python
class Solution:
    def nextPermutation(self, nums: 'List[int]') -> None:
        n=len(nums) 
        i = n-2
        while i>=0 and nums[i]>=nums[i+1]:# 添加重复元素出现的情况 eg：[5,1,1]
            i= i-1
            print(f'i {i}')

        if i==-1:         #对i进行处理,如果为倒序，直接反转
            nums.reverse()
        #测试用例通过264 ，其中从[100,99,...1]的d除了问题
        j = n-1
        while j>0 and nums[i]>=nums[j]: #添加重复元素存在的情况
            j = j-1
            print(f'nums[j] {nums[j]}')
        nums[j],nums[i]=nums[i],nums[j]

        left = i+1
        right= n-1
        while left<=right:
            nums[right],nums[left]=nums[left],nums[right]
            left = left+1
            right = right-1
```

最后对代码进行整合分类：
在遇到难题的时候，需要进行调试，以及练习试错，如果脑子里面觉得哪里有问题，在编码较少的情况下，光靠想象是无法调试问题的，需要进行实践，错误了就去查找原因。一步一步调试。思路有时候是乱的，但是只要慢慢一步一步的调试，总会有思路的。对于某些算法，原理层面上确实比较抽象，但是如果拆分步骤，慢慢逐步的调试，才能锻炼自己的编码能力。

```python
class Solution:
    def nextPermutation(self, nums: 'List[int]') -> None:
        n=len(nums)
        i = n-2
        while i>=0 and nums[i]>=nums[i+1]:# 添加重复元素出现的情况
            i= i-1
            print(f'i {i}')
        if i==-1:         #对i进行处理，倒序处理， 添加
            nums.reverse()
        else:
            j = n-1
            while j>0 and nums[i]>=nums[j]: #添加重复元素存在的情况，使用等号
                j = j-1
                print(f'nums[j] {nums[j]}')
            nums[j],nums[i]=nums[i],nums[j]
            left = i+1
            right= n-1
            while left<=right:
                nums[right],nums[left]=nums[left],nums[right]
                left = left+1
                right = right-1
```

==列表切片后，不能够使用reverse，查找切片的相关原理？==



#### 题号：60 顺序排序（Permutation Sequence）； 难度：==困难==  // 待定
顺序排序（Permutation Sequence）
//待定，知识点包含数组，但不仅仅只有数组，还有BFS（广度优先）。





#### 题号：36 验证数独（Valid Sudoku）；    难度：==中等==
验证数独（Valid Sudoku） 
个人思路：只需判断其是否有效，那么从三个维度去判断，所在行，所在列，以及所在的小方格中是否蛮子要求。那么具体判定，是否需要创建多少个dic进行判定，还是如何实现这种，建立多个dic合适？如何实现这个问题？没有思路。

官方思路：似乎并没有考虑空间复杂度，也没有自己想的那么难，直接使用空间，去装所有的状态，然后直接去判断。如果不要空间复杂度，那么这个计算难度就减少很多。
==对知识点字典，集合相关概念和操作不是很熟悉。以及结构化迭代==

该版本通过的测试用例有379/507,依然有部分测试用例未通过，查看一下什么情况

```python
class Solution:
    def isValidSudoku(self, board:'List[List[str]]') -> bool:
        rowCon=[[],[],[],[],[],[],[],[],[]]  #行数据列表，9个
        colCon=[[],[],[],[],[],[],[],[],[]]  #列数据列表，9个

        Smartix = [[[], [], []],             #方格数据，9个
                   [[], [], []],
                   [[], [], []]]
        rowN = len(board)
        colN = len(board[0])

        for row in range(0,rowN,1):
            for col in range(0,rowN,1):   #遍历数独
                
                if board[row][col]=='.':  #检测数据是否为数据
                    continue

                if board[row][col] in rowCon[row]:
                    return False
                else:
                    rowCon[row].append(board[row][col])

                if board[row][col] in colCon[col]:
                    return False
                else:
                    rowCon[col].append(board[row][col])  #错误原因：列向量为被压入列列表中。

                if board[row][col] in Smartix[row//3][col//3]:
                    return False
                else:
                    Smartix[row // 3][col // 3].append(board[row][col])

        return True
```

改正后代码：

```python
class Solution:
    def isValidSudoku(self, board:'List[List[str]]') -> bool:
        rowCon=[[],[],[],[],[],[],[],[],[]]  #行数据列表，9个

        colCon=[[],[],[],[],[],[],[],[],[]]  #列数据列表，9个

        Smartix = [[[], [], []],             #方格数据，9个
                [[], [], []],
                [[], [], []]]
        rowN = len(board)
        colN = len(board[0])

        for row in range(0,rowN,1):
            for col in range(0,rowN,1):   #遍历数独

                if board[row][col]=='.':  #检测数据是否为数据
                    continue

                if board[row][col] in rowCon[row]:
                     return False
                else:
                    rowCon[row].append(board[row][col])

                if board[row][col] in colCon[col]:
                    return False
                else:
                    colCon[col].append(board[row][col])

                if board[row][col] in Smartix[row//3][col//3]:
                    return False
                else:
                    Smartix[row // 3][col // 3].append(board[row][col])
        #print(f'the rowcon is {rowCon}')
        #print(f'the colCon con is {colCon}')
        #print(f'the Smartix is {Smartix}')
        return True

```

==如何y优化？==
使用自己的思路解题的时候，使用了大量的空间，但是逻辑比较清楚，简单粗暴，但是可以优化。主要是从空间复杂度进行优化。



#### 题号：42 收集雨水（Trapping Rain  Water）；   难度：==困难==  //待定，综合执要求

个人思路：暂无







#### 题号：48 旋转图像（Rotate Image）；   难度：==中等==   //待优化

题意：原地旋转，不要使用矩阵旋转，顺时针旋转90°。
个人思路：看似拿难度不大，主要是找关系。如果直接田添加一个空间，就比较简单，但是该题不允许添加空间。稍微要找一下问题的规律 。如果采用辅助内存：A\[row][col] = A1\[col][n-1-row]，整体来说空间复杂度占用高一点。
	不需要加内存的稍有点复杂，先写一版不加内存的。题目整体来说算是数学题，题目通过的时间复杂度和空间复杂度都比较低。

```python
class Solution:
	def rotate(self, matrix:'List[List[int]]') -> None:

		n=len(matrix)
		matrixTemp =[[(0)for i in range(n)]for i in range(n)] # [[0]*n]*n

		for row in range(n):
			for col in range(n):
				matrixTemp[col][n-1-row]=matrix[row][col]

		matrix[:]=matrixTemp   #   matrix=matrixTemp


		print(matrixTemp)


matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]

s1=Solution()
print(matrix)
s1.rotate(matrix)
print(matrix)
```

知识点 ：二维列表赋值问题。优化

#### 题号：66 加一运算（Plus One）；   难度：==简单==   //待优化

题意：将数拆开后，然后加以后在拆开进行返回。内存和执行时间都比较差，哪里还可以优化？

```python
class Solution:
    def plusOne(self, digits: 'List[int]') -> 'List[int]':
        newNumb= 0
        for i in digits:
            print(i)
            newNumb = newNumb*10+i
        newNumb= newNumb+1
        print(newNumb)

        NumbList =[]
        while(newNumb>0):
            NumbList.append(newNumb%10)
            newNumb = newNumb//10
        NumbList.reverse()
        return NumbList
```



#### 题号：70 爬楼问题（Climbing Stairs）；   难度：==简单==   

题意，到n个台阶有多少种爬楼方法。
个人思路：动态规划简单题，可以使用递归的方法

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n==1:
            return 1
        elif n==2:
             return 2
        else:
            return self.climbStairs(n-1)+self.climbStairs(n-2)   #类内部递归问题

n = 44
s1 = Solution()
print(s1.climbStairs(n))  #1134903170
```

存在问题：在递归的时候，测试在44的时候，其运算时间非常大，可以将其改为循环的情况，运算速度应该要好很多。

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        ClimbCon = 0
        if n==1:
            ClimbCon=1
            return ClimbCon
        if n==2:
            ClimbCon=2
            return
        else:
            LLlastN = 1
            LastN = 2
            for i in range(n-2):
                ClimbCon =LLlastN+LastN
                LLlastN = LastN    #小细节，赋值问题。从前到后，避免覆盖
                LastN=ClimbCon
        return ClimbCon
    
#44 1134903170
```

纯粹的循环问题，测试通过然后通过率垫底。基本无法优化。在python的对内存的优化作用不大，主要是对运行时间的优化最明显。底层的动态数据类型，使得其优化内存的作用并不大，主要还是针对于时间复杂度的优化。



#### 题号：89 格雷编码（Cray CODE ）；   难度：==中等==   

格雷码有通项：

```python
class Solution:
    def grayCode(self, n: int) -> List[int]:
        grayCodeList= []
        for i in range(2**n):
            grayCodeList.append(i^(i>>1))
        return grayCodeList

```



#### 题号：73 矩阵置零（ Set Matrix  Zeroes ）；   难度：==中等==   ==待优化==

   将数组置零有零的行和变成0
原地算法:一个原地算法(in-place algorithm)基本上不需要==额外辅助的数据结构==,然而,允许==少量额外的辅助变量==来转换数据的算法。
该题在解决过程中由于题目误读，导致其浪费了一段时间，但是中体来说，算法的效率较低，待优化。

```python
class Solution:
	def setZeroes(self, matrix: 'List[List[int]]') -> None:
		Matrixrow =len(matrix)  #行数
		Matrixcol =len(matrix[0]) #列数

		REValList =[]

		for i in range(0,Matrixrow):
			for j in range(0,Matrixcol):
				if matrix[i][j]==0:
					REValList.append([i,j])  #找出数组中为0的行列索引

		for i,j in REValList:
			for ColZero in range(Matrixcol): 
				matrix[i][ColZero] =0   #将i行置零
			for rowZero in range(Matrixrow):
				matrix[rowZero][j] = 0   #将j列置零
```



#### 题号：134 加油问题（Gas Station ）；   难度：==中等==   ==待优化 ，贪心？==

题意：判断加油站是否可以绕行一周，其环线是一个环形的。可以使用两个临时数组，将其存放，然后将其遍历进行判断。

暴力求解，算法解出来了，但是由于复杂度问题，在提交的时候，算法复杂度过高导致其超时。

```python
class Solution:
	def canCompleteCircuit(self, gas: 'List[int]', cost:'List[int]') -> int:

		gasN = len(gas)
		costN = len(cost)
		for i in range(gasN):
			startIndex = i
			newgasList = gas[i:gasN] + gas[0:i]
			newcostList = cost[(i):costN] + cost[0:(i)]
			oilN = 0

			#print(f'the newgasList is {newgasList}')
			#print(f'the newcostList is {newcostList}')

			for j in range(costN):
				#print(f'the j is {j}')
				oilN= newgasList[j]+oilN
				#print(f'the oilN is {oilN}')
				if oilN<newcostList[j]:
					break
				oilN=oilN-newcostList[j]
				if (j==costN-1 and 0<=oilN):
					return startIndex
		return -1


gas = [2,3,4]
cost = [3,4,3]
s1=Solution()
print(s1.canCompleteCircuit(gas,cost))

```

贪心法，解题，==未懂其原理==

```python
class Solution:
    def canCompleteCircuit(self, gas:'List[int]', cost: 'List[int]') -> int:
        if sum(gas)<sum(cost):
            return -1
        total = startIndex = 0
        for i in range(len(gas)):
            total = gas[i]-cost[i]+total
            if total<0:
                total =0
                startIndex = i+1
        return startIndex

```



#### 题号：455 分发饼干（assign cookies ）；   难度：==easy==   ==数组，贪心==

题意：分配饼干，使得更多的人吃饱。

贪心算法：贪心算法或贪心思想采用贪心的策略，保证每次操作的都是局部最优解的，从而使得得到的结果是全局最优。全局最优的结果是局部结果的简单求和，且==局部结果相互不相干==，因此局部最优解的策略也同样是全局最优解策略。
适用条件：局部结果不相干，求全局最优解

```python
class Solution:
    def findContentChildren(self, g: 'List[int]', s: 'List[int]') -> int:
        g.sort()
        s.sort()
        
        n =len(g)
        m = len(s)
        contNum = 0
        i,j =0,0
        while(i<n and j<m):
            if g[i]<=s[j]:
                contNum= contNum+1
                i = i +1
                j = j+1
            else:
                j = j+1    #由于是满足最大的人数，如果不满足，就一次将后面的饼给前面的人
        return contNum

```



#### 题号：135 分发糖果（candy ）；   难度：==困难==   ==待解决==







#### 题号：136 只出现一次的数字（Single Number  ）；   难度：==简单==   ==待解决==

再一个数组或者列表中，找出只出现一次的数字，其他都存在两次
要求：线性复杂度，不分配额外空间。先排序，然后找规律。从索引为0处开始找。

```python
class Solution:
    def singleNumber(self, nums: 'List[int]') -> int:
        nums.sort()
        print(nums)
        for i  in range(0,len(nums)-1,2):
            if nums[i]!=nums[i+1]:
                return nums[i]
        return nums[-1]

```

还可以使用异或，由于其他的两次，只有一个数字一个，直接用异或得出结果。非常拽。

```python
class Solution:
    def singleNumber(self, nums: 'List[int]') -> int:
        ret = 0
        for i  in range(0,len(nums)):
            ret =ret^nums[i]
        return ret
```



#### 题号：137 只出现一次的数字（Single Number II ）；   难度：==中等==  

将等于2的代码改成3，就通过

```python
class Solution:
    def singleNumber(self, nums: 'List[int]') -> int:
        nums.sort()
        print(nums)
        for i  in range(0,len(nums)-1,3): #3可以改成n，判断n个数中有一个数量为1.
            if nums[i]!=nums[i+1]:
                return nums[i]
        return nums[-1]

```








### 链表：调试不好调试，后序在写

#### 题号：21 合并链表；   难度：==简单==  

```python
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        dump =ListNode(-1)
        p=dump
        while(l1 and l2):
            if(l1.val<=l2.val):
                p.next=l1
                l1=l1.next
            else:
                p.next=l2
                l2=l2.next
            p=p.next
        p.next = l1 if l1 is not None else l2
        return dump.next
```

python代码中，主要是通过类的模拟进行链表建立，在本体题目中，有三个细节
1.类为None是什么意思 ：类内部的元素next的指向是为空的，其中
2.类的赋值是情况是深拷贝还是引用：类似指针为浅拷贝
3.语法问题。 与lambda函数类似，或者说三目运算符。





##  字符串

#### 题号：28 实现str（）；   难度：==简单==     KMP

算法实现了，但是算法时间超时，不知道结果能不能通过，理论上是能够通过的，也算是暴力解法的一种，本题的重点是KMP。

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        strN1 = len(haystack)
        strN2 = len(needle)
        if strN2==0:
            return 0
        i = 0
        j = 0
        while(i<strN1):
            if (j<strN2 and haystack[i]==needle[j]):#测试用例      
                i =i+1
                j =j+1       
            else:
                i = i-j+1   #细节问题，如果两句交换，结果会出问题
                j = 0
            if j==strN2:
                return (i-j)
        return -1

haystack = "aaa"
needle = "aaa"

s1 = Solution()
print(s1.strStr(haystack,needle))
```

直接使用库函数，通过率和效率都比较高，说明python底层的字符匹配算法效率比较高。

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        return haystack.find(needle)

haystack = "aaa"
needle = "aaa"

s1 = Solution()
print(s1.strStr(haystack,needle))
```

试试使用KMP算法。该算法原理不太清楚，但是使用的时候难度不大。

```python
#原理
概念：最长公共前后缀表:最长公共前后缀的交集。
eg：[a,b,a,b,c]  最长公共前后缀表 [0,0,1,2,0]  #有时候为了方便编程，会将数组右移一位，首元素置-1。
最长公共前后缀列表：  prefix table
子串		 数量			 最长前缀     最长后缀
          
a          0   #无后缀                             
a b        0
a b a      1    a
a b a b    2    a，b     a，b，a    b，a，b
a b a b c  0             a,b,a,b   b,a,b,c
```

对于kmp算法中，设主字符串为p，需要查找的字符为l，主要是通过l的prefix table，在主字符串中进行匹配，通过prefixtable 减少查找次数，主要算法两个部分，一个是prefixtable，一个是匹配过程：

对于prefixtable（next数组）部分：

![010FD8AE2B79FFE03DC3735ACD224A6A.png](Leetcode .assets/KMP_prefixtable.png)

![prefixtable2](Leetcode .assets/prefixtable2.png)

![prefixtable3](Leetcode .assets/prefixtable3.png)

![prefixtable4](Leetcode .assets/prefixtable4.png)



KMP速度快的原因
1.KMP 利用已匹配部分中相同的「前缀」和「后缀」来加速下一次的匹配。
2.KMP 的原串指针不会进行回溯（没有朴素匹配中回到下一个「发起点」的过程）。

```python
class Solution:   #本代码将c++ 代码进行移植过来，KMP算法需要进行消化，原理上比较简单，但是也需要理解
    def prefixTableList(self,substring):  #将最大公共前后缀的数组。（next数组构建）
        i = 1
        j = 0
        m = len(substring)
        prefixTable =[0]*m     #next 数组  
        while(i<m):
            while(j>0 and substring[i]!=substring[j]):#
                j = prefixTable[j-1]
            if(substring[i]==substring[j]):
                j = j+1
            prefixTable[i] = j
            i = i +1
        return prefixTable

    def kmpAlgorithnm(self,string,substring): #使用两个数组进行对比。kmp比暴力算法节约时间的地方就在于对比到两个字符不想等的时候，不用从新开始对比，而是使用prefix的索引进行对比，使得算法的效率较高
        n = len(string)
        m = len(substring)
        prefix = self.prefixTableList(substring)

        i ,j = 0 ,0   #i指向主串， j指向子串
        while( i<n and j<m ):
            while(j>0 and string[i]!=substring[j]):
                j = prefix[j-1]
            if(string[i]==substring[j]):
                j = j+1
            if(j==m):
                return i-m+1
            i = i+1
        return -1
      
    def strStr(self, haystack: str, needle: str) -> int:
        if len(needle)==0:
            return 0
        return  self.kmpAlgorithnm(haystack,needle)

haystack = "mississippi"
needle = "pi"

s1 = Solution()
print(s1.strStr(haystack,needle))
```



#### 题号：8 字符串转化为整型；   难度：==中等==       //待解决

本体属于细节题，其中很多测试用例比较复杂，需要对齐状态进行思考，其中字符串由英文字符，数字0-9，以及
’.‘,'+'."-"组成，那么怎么编写呢？细节太多

思考编写了一版，思路较乱，然后测试用例通过较少，像修墙一样，有问题。

```python
class Solution:
	def myAtoi(self, s: str) -> int:
		newStr=s.replace(' ','')  #replace函数可以删除特定的字符串
		print(f'the newstr is {newStr}')
		n = len(newStr)
		if n==0:       #处理空串的情况
			return 0
		#处理一个字符，单字符为’+‘，’-‘和str的情况
		if (n==1)  and	(newStr[0].isalpha() or newStr[0]=='+' or newStr[0]=='-'):
			return 0
		#处理+-号同时在的情况
		if ('+'  in newStr) and ('-'  in newStr):  #不等于语法： ’+‘ and '-' in newstr
			return 0

		endIndex = 0
		for i in range(n):
			if newStr[0].isalpha():
				return 0
			if (not newStr[i].isalpha()):
				endIndex = i
			else:
				break
		startIndex = 0
		newStr = newStr[:endIndex + 1]      #该字符串包含’+‘或’-‘ 以及数字组成
		'''  该段处理类似"00000-42a1234"，为-42，但是测试用例为0
		for j in  range(len(newStr)):
			if newStr[j]!='0':
				startIndex =j
				break
		newStr = newStr[startIndex:]
		print(f'the newstr3 is {newStr}')
		'''
		if '-' in newStr and newStr[0]!='-':
			return 0

		if '.' in newStr:   #判断是否由小数
			Num = float(newStr)
			Num = int(Num)
		else:
			Num = int(newStr)

		if Num<=-2**31:    #边界判定
			Num = -2**31
		if Num>=2**31-1:
			Num=2**31-1
		return Num

print(-2**31)       # 符号优先级问题，其中负号的优先级比较低
print(+23)            #如果带符号，正号会直接省略
print(int(' 3'))   #将数字字符串强制转成int的时候，空格不受影响
s="     +004500"
s1=Solution()

print(s1.myAtoi(s))

#00000-42a1234
```

算法未通过：有问题，该题难度很大，花了四，五个小时未能解答，试试看解题思路，以及该状态解法

#### 题号：67 二进制求和；   难度：==简单==       

题意：非空字符串，将两个非空字符串（二进制想加），然后返回二进制和

个人解题思路，头脑有点转不过来，简单题测试用例通过293/294,唯一没有通过的测试用例为‘0’，‘0’的时候

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        n1 = len(a)
        n2=len(b)
        a1,b1 = 0,0
        for i in a:
            a1 = int(i)*2**(n1-1)+a1
            n1= n1-1
        print(a1)
        for j in b:
            b1 = int(j)*2**(n2-1)+b1
            n2= n2-1
        print(b1)
        c=a1+b1
        print(c)
        cList = []
        while(c>0):
            cList.append(c%2)
            c=c//2
        print(cList)
        cList.reverse()
        srtList = ''
        for i in cList:
            srtList= srtList+str(i)
        return srtList
```

```python
class Solution: #代码通过，但是是分臃肿，十分乱
    def addBinary(self, a: str, b: str) -> str:
        n1 = len(a)
        n2=len(b)
        a1,b1 = 0,0
        for i in a:
            a1 = int(i)*2**(n1-1)+a1
            n1= n1-1
        print(a1)
        for j in b:
            b1 = int(j)*2**(n2-1)+b1
            n2= n2-1
        print(b1)
        c=a1+b1
        print(c)
        cList = []
        if c == 0:   #处理c为0的情况
            cList.append(0)
            print(cList)
        else:
            while(c):
                cList.append(c%2)
                c=c//2
        cList.reverse()
        srtList = ''
        for i in cList:
            srtList= srtList+str(i)
        return srtList
```

题解方法：积累状态。
