```bash
-b, --ignore-leading-blanks    忽略开头的空白。
-d, --dictionary-order         仅考虑空白、字母、数字。
-f, --ignore-case              将小写字母作为大写字母考虑。
-g, --general-numeric-sort     根据数字排序。
-i, --ignore-nonprinting       排除不可打印字符。
-M, --month-sort               按照非月份、一月、十二月的顺序排序。
-h, --human-numeric-sort       根据存储容量排序(注意使用大写字母，例如：2K 1G)。
-n, --numeric-sort             根据数字排序。
-R, --random-sort              随机排序，但分组相同的行。
--random-source=FILE           从FILE中获取随机长度的字节。
-r, --reverse                  将结果倒序排列。
--sort=WORD                    根据WORD排序，其中: general-numeric 等价于 -g，human-numeric 等价于 -h，month 等价于 -M，numeric 等价于 -n，random 等价于 -R，version 等价于 -V。
-V, --version-sort             文本中(版本)数字的自然排序。
```