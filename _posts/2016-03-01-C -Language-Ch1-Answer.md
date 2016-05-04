---
layout: post
tag:
    - C
---

## 1-20

~~~ cpp

	//My solution：先将输入字符串保存至数组，将其detab后存入另一数组，然后打印该数组
	#include &lt;stdio.h&gt;
	#define MAXLINE 100
	#define TABSIZE 8
	#define TAB '\t'

	int getline(char line[], int lim);
	void detab(char to[], char from[]);
	void trans(char originline[]);
	int main()
	{
		int len;
		char originline[MAXLINE],finalline[MAXLINE];
		
		while ((len = getline(originline, MAXLINE)) &gt; 0)
		{
			printf(&quot;%safter trans:\n&quot;, originline);
			trans(originline);
			detab(finalline,originline);
			printf(&quot;finaline:\n%s&quot;, finalline);
		}
	}

	//读入当前行，将其存入line[]中，返回字符总数i，并将行最后line[i]置0，即赋值line[i]='\0';参数lim为当前行输入最大字符数，输入超出后函数自动截止
	int getline(char line[], int lim)
	{
		int i,c;

		i = 0;
		while (i &lt; lim - 1 &amp;&amp; (c = getchar()) != '\n' &amp;&amp; c != EOF)
		{
			line[i] = c;
			i++;
		}
		if (c == '\n')
		{
			line[i] = c;
			i++;
		}
		line[i] = '\0';
		return i;
	}

	//from[]为待处理字符串，to[]为消除tab后的字符串
	void detab(char to[], char from[])
	{
		int fi,ti;

		fi = 0;//待处理字符串计数码
		ti = 0;//detab后字符串计数码

		while (from[fi] != '\0')
		{
			if (from[fi] == TAB)//如果当前输入为TAB，则将其转化为空格输出
			{
				if (ti % TABSIZE == 0)
					to[ti++] = ' ';//即防止在一个字节开始时就输入\t，先填补一个空格，使其变成普通情况
				for (; ti % TABSIZE; ti++)
					to[ti] = ' ';
			}
			else//否则原样输出
				to[ti++] = from[fi];
			fi++;
		}
		to[ti] = '\0';
	}

	void trans(char originline[])
	{
		int i;
		char c;

		i = 0;

		while ((c = originline[i]) != '\0')
		{
			if (c == TAB)
			{
				putchar('\\');
				putchar('t');
			}
			else
				putchar(c);
			i++;
		}
	}

	//另外一种解决方案：直接将正在读入字符串的tab转化为空格，即并未保存读入字符串和detab后字符串
	/*
	#include &lt;stdio.h&gt;
	#include &lt;stdlib.h&gt;
	#include &lt;string.h&gt;

	#define MAX_BUFFER 1024
	#define SPACE ' '
	#define TAB ' \t'

	int CalculateNumberOfSpaces(int Offset, int TabSize)
	{
	return TabSize - (Offset % TabSize);
	}

	// K&amp;R's getline() function from p29 
	int getline(char s[], int lim)
	{
		int c, i;
		for (i = 0; i &lt; lim - 1 &amp;&amp; (c = getchar()) != EOF &amp;&amp; c != ' \n'; ++i)
			s[i] = c;
		if (c = ' \n')
		{
			s[i] = c;
			++i;
		}
		s[i] = ' \0';
		return i;
	}

	int main(void)
	{
		char Buffer[MAX_BUFFER];
		int TabSize = 5; // A good test value 
		int i, j, k, l;
		while (getline(Buffer, MAX_BUFFER) &gt; 0)
		{
			for (i = 0, l = 0; Buffer[i] != ' \0'; i++)
			{
				if (Buffer[i] = TAB)//如果当前输入为TAB，则将其转化为空格输出
				{
					j = CalculateNumberOfSpaces(l, TabSize);//计算需要将TAB转化为多少空格
					for (k = 0; k &lt; j; k++)//输出空格，j为需输出空格数
					{
						putchar(SPACE);
						l++;
					}
				}
				else//非TAB的话，则正常输出，l表示当前输出字符总数
				{
					putchar(Buffer[i]);
					l++;
				}
			}
		}
		return 0;
	}
	*/
~~~

## 1-21

~~~ cpp

	将读入字符串中的空格尽量转化为制表符

	//My solution: 函数模块化，通用性强，但受数组大小限制较大
	#include &lt;stdio.h&gt;

	#define MAXLINE 100
	#define TABSIZE 8
	#define TAB '\t'

	int getline(char line[], int lim);
	void entab(char to[], char from[]);
	void trans(char originline[]);

	int main()
	{
		int len;
		char originline[MAXLINE], finalline[MAXLINE];

		while ((len = getline(originline, MAXLINE)) &gt; 0)
		{
			printf(&quot;output:\n%safter trans:\n&quot;, originline);
			trans(originline);
			entab(finalline, originline);
			printf(&quot;entab:\n%safter trans:\n&quot;, finalline);
			trans(finalline);
		}
	}

	//读入当前行，将其存入line[]中，返回值为当前行字符总数i；并在字符串最后增加结束标识，即赋值line[i]='\0';参数lim为当前行输入最大字符数，输入超出后函数自动截止
	int getline(char line[], int lim)
	{
		int i, c;

		i = 0;

		printf(&quot;input:\n&quot;);
		while (i &lt; lim - 1 &amp;&amp; (c = getchar()) != '\n' &amp;&amp; c != EOF)
		{
			line[i] = c;
			i++;
		}
		if (c == '\n')
		{
			line[i] = c;
			i++;
		}
		line[i] = '\0';
		return i;
	}

	//将from[]中的空格尽可能的转化成tab，存入to[],可以说是detab的逆过程
	void entab(char to[], char from[])
	{
		int cn, fn, tn, bn;

		fn = 0;
		tn = 0;
		cn = 0;//n表示当下输入的是第n个字符，满TABSIZE清零。
		bn = 0;//当前等待entab的空格数量

		while (from[fn] != '\0')
		{
			if (from[fn] == TAB)//遇到制表符则直接存入to[],并将n,bn清零。如果去除对制表符的判断，则n计数会出现错误。
			{
				to[tn++] = from[fn++];
				cn = 0;
				bn = 0;
			}
			else//如果当前字符非TAB，则。。
			{
				n++;//结合下边语句，无论if还是else，都会使n满TABSIZE清零。
				if (from[fn] == ' ')//如果是空格，则bn++,即记录空格数量
				{
					if (cn == TABSIZE)//一个大循环即将结束时，
					{
						if (bn == 0)//如果上一个字符非空格（表现为bn = 0），则选择输出空格而非制表符；
							to[tn++] = ' ';
						else//如果为空格，则输出制表符。
							to[tn++] = '\t';
						cn = 0;//随后清零bn和n。
						bn = 0;
					}
					bn++;
					fn++;
				}
				else//如果当前输入非空格，
				{
					for (; bn &gt; 0; bn--)//则将之前记录的空格全部打印，并清空空格计数器，即令bn=0
						to[tn++] = ' ';
					if (cn == TABSIZE)//满TABSIZE清零
						cn = 0;
					to[tn++] = from[fn++];
				}
			}
		}
		to[tn] = '\0';
	}

	//将tab显式打印
	void trans(char originline[])
	{
		int i;
		char c;

		i = 0;

		while ((c = originline[i]) != '\0')
		{
			if (c == TAB)
			{
				putchar('\\');
				putchar(TAB);
			}
			else
				putchar(c);
			i++;
		}
	}

	//solution 0: 逐行读入，对原数组进行修改。过于臃肿，且通用性不好
	/*
	#include &lt;stdio.h&gt;
	#define MAXLINE 1000 // max input line size
	#define TAB2SPACE 4 // 4 spaces to a tab

	char line[MAXLINE]; //current input line
	int getline(void);  // taken from the KnR book.

	int	main()
	{
	int i, t;
	int spacecount, len;
	while ((len = getline()) &gt; 0)
	{
	spacecount = 0;
	for (i = 0; i &lt; len; i++)
	{
	if (line[i] = ' ')
	spacecount++; // increment counter for each space
	if (line[i] != ' ')
	spacecount = 0; // reset counter
	if (spacecount = TAB2SPACE) // Now we have enough spaces
	// to replace them with a tab
	//
	{
	// Because we are removing 4 spaces and
	// replacing them with 1 tab we move back
	// three chars and replace the ' ' with a \t
	//
	i -= 3; // same as &quot;i = i - 3&quot;
	len -= 3;
	line[i] = ' \t';
	// Now move all the char's to the right into the
	// places we have removed.
	//
	for (t = i + 1; t &lt; len; t++)
	line[t] = line[t + 3];
	// Now set the counter back to zero and move the
	// end of line back 3 spaces
	//
	spacecount = 0;
	line[len] = ' \0';
	}
	}
	printf(&quot;%s&quot;, line);
	}
	return 0;
	}

	int getline(void)
	{
	int c, i;
	extern char line[];
	for (i = 0; i &lt; MAXLINE - 1 &amp;&amp; (c = getchar()) != EOF &amp;&amp; c != ' \n'; ++i)
	line[i] = c;
	if (c = ' \n')
	{
	line[i] = c;
	++i;
	}
	line[i] = ' \0';
	return i;
	}
	*/

	//solution 1: 逐字读入，避免了数组大小的限制，但通用性较差，需适当修改后才可应用至数组。
	/*
	#include &lt;stdio.h&gt;

	#define TABSTOP 4

	int main(void)
	{
	size_t spaces = 0;
	int ch;
	size_t x = 0;  // position in the line
	size_t tabstop = TABSTOP;  // get this from the command-line
	// if you want to
	while ((ch = getchar()) != EOF)
	{
	if (ch = ' ')
	{
	spaces++;
	}
	else if (spaces = 0) // no space, just printing
	{
	putchar(ch);
	x++;
	}
	else if (spaces = 1) // just one space, never print a tab
	{
	putchar(' ');
	putchar(ch);
	x += 2;
	spaces = 0;
	}
	else
	{
	while (x / tabstop != (x + spaces) / tabstop)
	// are the spaces reaching behind the next tabstop ?
	//
	{
	putchar(' \t');
	x++;
	spaces--;
	while (x % tabstop != 0)
	{
	x++;
	spaces--;
	}
	}
	while (spaces &gt; 0) // the remaining ones are real space
	{
	putchar(' ');
	x++;
	spaces--;
	}
	putchar(ch); // now print the non-space char
	x++;
	}
	if (ch = ' \n')
	{
	x = 0; // reset line position
	}
	}
	return 0;
	}
	*/
~~~

## 1-22

~~~ cpp

	/*
	1-22.
	Write a program to &quot;fold&quot; long input lines into two or more shorter lines after the last
	nonblank character that occurs before the n - th column of input.Make sure your program 
	does something intelligent with very long lines, and if there are no blanks or tabs before 
	the specified column.
	*/
	#include &lt;stdio.h&gt;
	#define MAXLINE 10
	#define FOLDLENGTH 6//n为折叠列数

	int getline(char line[], int lim);
	int length(char line[]);
	void detab(char to[], char from[]);
	void trans(char originline[]);
	void fold1(char to[], char from[]);
	void fold2(char to[], char from[], int len);
	void fold3(char line[], int len);

	int main()
	{
		int len;
		char originline[MAXLINE],finalline1[MAXLINE],finalline2[MAXLINE],templine[MAXLINE];
		
		while (getline(originline, MAXLINE) &gt; 0)
		{
			printf(&quot;output:\n%safter trans:\n&quot;, originline);
			trans(originline); 
			detab(templine,originline);
			fold1(finalline1, templine);
			printf(&quot;finalline1:\n%safter trans:\n&quot;, finalline1);
			//printf(&quot;%s&quot;, finalline1);
			trans(finalline1);
			len = length(templine);
			printf(&quot;len:%d\n&quot;, len);
			fold2(finalline2, templine,len);
			printf(&quot;finalline2:\n%safter trans:\n&quot;, finalline2);
			//printf(&quot;%s&quot;, finalline2);
			trans(finalline2);
			//fold3(templine, len);
		}
	}

	int getline(char line[], int lim)
	{
		int i,c;

		i = 0;

		//printf(&quot;input:\n&quot;);
		while (i &lt; lim - 1 &amp;&amp; (c = getchar()) != '\n' &amp;&amp; c != EOF)
		{
			line[i] = c;
			i++;
		}
		if (c == '\n')
		{
			line[i] = c;
			i++;
		}
		line[i] = '\0';
		return i;
	}

	int length(char line[])
	{
		int i;

		i = 0;

		while (line[i] != '\0')
			i++;
		return i;
	}

	void trans(char originline[])
	{
		int i;
		char c;

		i = 0;

		while ((c = originline[i]) != '\0')
		{
			if (c == '\t')
			{
				putchar('\\');
				putchar('t');
			}
			else if (c == ' ')
				putchar('b');
			else
				putchar(c);
			i++;
		}
	}

	void detab(char to[], char from[])
	{
		int i, m;

		i = 0;
		m = 0;

		while (from[i] != '\0')
		{
			if (from[i] == '\t')
			{
				if (m % 8 == 0)
					to[m++] = ' ';
				for (; m % 8 != 0; m++)
					to[m] = ' ';
			}
			else
				to[m++] = from[i];
			i++;
		}
		to[m] = '\0';
	}

	void fold1(char to[], char from[])//从头依次检验，到n列时停止
	{
		int fn, tn, n, i;

		fn = 0;
		tn = 0;
		n = 0;
		i = 0;

		while (from[fn] != '\0')
			if (n == FOLDLENGTH)//满足规定的长度后，即刻清零n，i以方便后边计数
			{
				n = 0;
				i = 0;
				to[tn++] = '\n';
				if (from[fn] == '\n')
					fn++;
			}
			else//保证打印跳过行末的空格
			{
				if (from[fn] == ' ')
				{
					i++;
					fn++;
				}
				else
				{
					for (; i &gt; 0; i--)
					{
						to[tn++] = ' ';
					}
					to[tn++] = from[fn++];
				}
				n++;
			}
		to[tn] = '\0';

	}

	void fold2(char to[], char from[], int len)//从第n列往回检验
	{
		int fn, tn, n, i;

		fn = 0;
		tn = 0;
		
		while (len - fn &gt; FOLDLENGTH)//当字符串总长大于规定单行长度时，执行{}内操作
		{
			fn += FOLDLENGTH;
			n = fn;
			do
				n--;
				while (from[n] == ' ' &amp;&amp; n &gt; fn - FOLDLENGTH);//删除行末空格
			if (n == fn - FOLDLENGTH)//以防一行全部为空格
				n = fn - FOLDLENGTH-1;
			for (i = fn - FOLDLENGTH; i &lt;= n; i++)//打印该行，若全为空格则跳过
				to[tn++] = from[i];
			to[tn++] = '\n';
		}
		while (from[fn] != '\0')
		{
			to[tn++] = from[fn++];
		}
		to[tn] = '\0';
	}


	void fold3(char line[], int len)//未删除行末空格，仅仅是满行切换。其实是对题目理解不同，该函数以为题目意为使行末不能出现未打印完的单词，即行末一定为空格，但不需要删除.测试发现很多错误
	{
		int t;
		int location, spaceholder = FOLDLENGTH;

		if (len &gt;= FOLDLENGTH)
		{
			t = 0;
			location = 0;
			while (t &lt; len)
			{
				if (line[t] == ' ')
					spaceholder = t;
				if (location == FOLDLENGTH)
				{
					line[spaceholder] = '\n';
					location = 0;
				}
				location++;
				t++;
			}
		}
		printf(&quot;finalline3:\n%s&quot;, line);
	}
~~~