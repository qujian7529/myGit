## Vim使用
i：在当前字符的左边插入  
I：在当前行首插入  
a：在当前字符的右边插入  
A：在当前行尾插入  
o：在当前行下面插入一个新行  
O：在当前行上面插入一个新  
h: 向前移动一个字符  
j: 向上移动一行  
k: 向下移动一行  
l: 向后移动一个字符  
yy: 复制当前一行  
dd:剪切当前一行  
p: 粘贴内容到游标之后  
P: 粘贴内容到游标之前  
## 文件　
vim file  /  touch file 创建文件  
cp file file1 复制  
cp file  /home/linux/file1 复制到..  
cat file 查看  
mv file /home/linux/  移动
mv file file2　重命名
## 目录
mkdir dir　创建目录
cp dir   dir1  -a　复制
cp dir   /home/linux/dir2  -a　复制到..
mv dir  dir2　重命名
mv dir  /home/linux/　移动
rm  dir  -rf　删除
ls -d  dir　查看
find  ./dir  -name  "filename"　查看
## 文件压缩归档
