# Bugku-散乱的密文 WriteUp

## 题目信息
- 题目名称：散乱的密文
- 题目类型：Crypto
- 题目来源：Bugku CTF
- 密文：If5{ag024c483549d7fd@@1}
- 提示：置换顺序 2 1 6 5 3 4

## 解题思路
题目给出的数字序列为 **6位分组置换规则**，含义为每6个字符为一组，按照顺序 `2 1 6 5 3 4` 进行位置打乱。
将规则转为程序下标（从0开始）加密顺序：`[1, 0, 5, 4, 2, 3]`。
通过逆置换恢复每组字符顺序即可得到明文，最后剔除干扰字符 @@。

## EXP
```python
cipher = "If5{ag024c483549d7fd@@1}"
order = [1, 0, 5, 4, 2, 3]
res = ""

for i in range(0, len(cipher), 6):
    block = cipher[i:i+6]
    if len(block) == 6:
        block = ''.join([block[x] for x in order])
    res += block

print(res)
