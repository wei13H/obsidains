1.赋值符 “ = ” 
name = zzk
 curname = $(name)
 name = zuozhongkai
	@echo curname: $(curname)
	最后输出的是curname ：zuozhongkai
这就是赋值符“=”的神奇之处！借助另外一个变量，可以将变量的真实
值推到后面去定义。也就是变量的真实值取决于它所引用的变量的最后一次有效值1
2.赋值符 “：= ”
name = zzk
curname := $(name)
name = zuozhongkai
print:
@echo curname: $(curname)
输出结果是curname ：zzk
3.赋值符 “ ？= ”
