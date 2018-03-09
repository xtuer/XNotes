```cpp
char chs[] = {0x0A, 0x0B, 0x0C, 0x0D, 0x0E};
QByteArray ba(chs, 5);
// ba.append(0x0A).append(0x0B).append(0x0C).append(0x0D);

for (int i = 0; i < ba.size(); ++i) {
    std::cout << (int)ba.at(i) << " "; // 10 11 12 13 14 
}

std::cout << std::endl;

// 168496141
qDebug() << qFromBigEndian<qint32>((const uchar *)chs); // 168496141
qDebug() << ((0x0A << 24) | (0x0B << 16) | (0x0C << 8) | 0x0D); // 168496141

qToBigEndian(qint32(168496141), (uchar *)chs);
for (int i = 0; i < 5; ++i) {
    std::cout << (int)chs[i] << " "; // 10 11 12 13 14
}

// ba.setNum(123456789); // 不是 4 个字节，而是把这个整数保存为 9 个字符 1 到 9

--------------------------------------------------------------
输出:
10 11 12 13 14 
168496141
168496141
10 11 12 13 14
```



