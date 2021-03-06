## UTF-8 的编码规则

我们通常说，UTF-8 字符集的汉字，每一个字占 3 个字节。我们并没有说过 UTF-8 字符集的一个字符都是 3 个字节。UTF-8 是一种变长字节编码方式，它的长度从 1~6 个字节都是合法的编码范围。

对于某一个字符的 UTF-8 编码:

* 只有一个字节则其最高二进制位为 0，为了兼容 ASCII 码
* 多字节，其第一个字节从最高位开始，二进制位中连续的 1 的个数决定了其编码的位数，其余各字节均以 10 开头

UTF-8 最多可用到 6 个字节，具体可以参看下表：

| utf-8的字节数\(byte\) | 有效数据位\(bit\) |
| :--- | :--- |
| 1 | 0xxxxxxx |
| 2 | 110xxxxx 10xxxxxx |
| 3 | 1110xxxx 10xxxxxx 10xxxxxx |
| 4 | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx |
| 5 | 111110xx 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx |
| 6 | 1111110x 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx |

我们来数一下 x 的数量，也就是每一种编码规则包含的有效数据位：

| utf-8的字节数\(byte\) | 有效数据位\(bit\) |
| :--- | :--- |
| 1 | 7 |
| 2 | 5+6=11 |
| 3 | 4+6\*2=16 |
| 4 | 3+6\*3=21 |
| 5 | 2+6\*4=26 |
| 6 | 1+6\*5=31 |

那么，如果需要编码的 bit 数大于可以编码的 bit 数，则该编码方案无效。

假设需要编码的数据位为 6 bits，那么这个六种方案都可以编码；如果需要编码的数据位为 27 bits，那么只有 6 字节方案可以编码。

但事与愿违，抛开浪费空间不说，如果我们把 3 字节汉字的数据位前面强行置 0，让它以 4 字节编码，数据转换过程还是会破坏，这里留一个疑问。

那么，4 字节字符到底是什么？Emoji，所谓 Emoji 就是一种在 Unicode 位于`\u1F601-\u1F64F`区段的字符，这个显然超过了目前常用的 UTF-8 字符集的编码范围`\u0000-\uFFFF`。

如 "{\(byte\)0xF0,\(byte\)0x9F,\(byte\)0x98,\(byte\)0x81}" 表示一个笑脸。

言归正传，实际上我们关注的是 Unicode 和 UTF-8 之间的关系：

| Unicode符号范围 | UTF-8编码方式 |
| :--- | :--- |
| 0000 0000-0000 007F | 0xxxxxxx |
| 0000 0080-0000 07FF | 110xxxxx 10xxxxxx |
| 0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx |
| 0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx |



