<div align="center">

## Variable length argument lists


</div>

### Description

After looking at functions like printf() and scanf() and their ability to accept any number of arguments I got curious to see how its done. This article explains how to create a function that will allow any number of parameters to be passed to it, and ho to accept those extra parameters.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jason Beighel](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jason-beighel.md)
**Level**          |Intermediate
**User Rating**    |5.0 (25 globes from 5 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, UNIX C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jason-beighel-variable-length-argument-lists__3-3299/archive/master.zip)





### Source Code

<p>In C it is possible to create a function that will accept a variable amount of arguments. The parameter must have at least one defined parameter followed by an ellipsis, three periods “…”. For example printf()’s prototype has one defined parameter and an ellipses:</p>
<p>printf(char *, …);</p>
<p>However, just an ellipses is not allowed:</p>
<p>function(…);</p>
<p>You may use as many defined arguments as you would like, but the ellipses must be the last, for example:</p>
<p>function(int, char *, float, …);</p>
<p>There are several functions used to access the arguments passed through the ellipses, to use them you must include cstdarg.</p>
<p>	#include<cstdarg></p>
<p>Note that cstdarg is not a header file, but it is included like one.</p>
<p>In the function that is receiving the variable arguments you must have a va_list variable that is used by the functions that retrieve the arguments passed through the ellipses. The function va_start() will setup the va_list variable so you can retrieve arguments. The va_start() function takes two arguments. The first is the va_list variable, and the second is the argument that immediately precedes the variable arguments.</p>
<p>The function used to actually retrieve the arguments is va_arg(). This function also takes two arguments. The first is a va_list variable that has previously established with va_start(), and the second is the type of variable you want to retrieve. For the type you use any variable type; for example int or char. The va_arg() function will return the value of the variable you are retrieving.</p>
<p>When you are done you must call va_end() to clean up the va_list variable. It only takes a va_list variable.</p>
<p>Here is an example of all that put together:</p>
<p>#include&lt;cstarg&gt;</p>
<p>#include&lt;stdio.h&gt;</p>
<p>void VarArg(int Num, …);</p>
<p>void main(void)</p>
<p>{</p>
<p>	VarArg(4, 1, 2, 3, 4);</p>
<p>	VarArg(3, 6, 7, 8);</p>
<p>	return;</p>
<p>}</p>
<p>void VarArg(int Num, …)</p>
<p>{</p>
<p>	va_list VList;</p>
<p>	va_start(VList, Num);</p>
<p>	printf(“\nPassed parameters: “);</p>
<p>	for (; Num > 0; Num--)</p>
<p>{</p>
<p>	printf(“ %d,”, va_arg(VList, int);</p>
<p>}</p>
<p>return;</p>
<p>}</p>

