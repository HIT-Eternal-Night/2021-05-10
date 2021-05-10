# 2021-05-10
排序与查找，最后的试炼！

1、冒泡排序法。设有N（N为5）个杂乱无序的整数，要求将这N个整数从小到大排序后输出。
**输入格式要求："%d" 提示信息："Enter No.%2d:"
**输出格式要求："%d"
程序运行示例如下：
Enter No. 1:5
Enter No. 2:7
Enter No. 3:3
Enter No. 4:9
Enter No. 5:8
35789
我的答案：
#include<stdio.h>
#define N 5

void BubbleSort(int a[], int n);
void Swap(int *p1,int *p2);

int main(int argc,char const*argv[])
{
	int a[N];
	int i;
	
	for (i=0 ; i<N ; i++)
	{
		printf("Enter No.%2d:",i+1);
		scanf("%d",&a[i]);
	}
	
	BubbleSort(a,N);
	
	for (i=0 ; i<N ; i++)
	{
		printf("%d",a[i]);
	}
	
	return 0;
}

void swap(int *p1,int *p2)
{
	int temp;
	temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}

void BubbleSort(int a[], int n)
{
	int i,j;
	for (i=0 ; i<N-1 ; i++)
	{
		for (j=0 ; j<N-1-i ; j++)
		{
			if (a[j] > a[j+1])
			{
				swap(&a[j],&a[j+1]);
			}
		}
	}
}

总结：看清题目：No.12345。冒泡排序的要点：i<N-1,j<N-1-i

2、采用冒泡法进行升序排序。
基本原理是：对数组中的n个数执行n-1遍检查操作，在每一遍执行时，对数组中剩余的尚未排好序的元素进行如下操作：
对相邻的两个元素进行比较，若排在后面的数小于排在前面的数，则交换其位置，
这样每一遍操作中都将参与比较的数中的最大的数沉到数组的底部，经过n-1遍操作后将全部n个数按从小到大的顺序排好序。
要求限制数组元素最大个数为10。

程序的某次运行结果如下：
Input n:5↙
Input 5 numbers:21 32 45 12 0↙
Sorting results:   0  12  21  32  45（换行）

输入格式:"%d"
输入数据个数提示："Input n:"
输入数据提示："Input %d numbers:"
输出提示："Sorting results:"
输出数据格式:"%4d"

我的答案：
#include<stdio.h>

void BubbleSort(int a[], int n);
void Swap(int *p1,int *p2);

int main(int argc,char const*argv[])
{
	int i,n;
	int a[n];
	
	printf("Input n:");
	scanf("%d",&n);
	
	printf("Input %d numbers:",n);
	for (i=0 ; i<n ; i++)
	{
		scanf("%d",&a[i]);
	}
	
	BubbleSort(a,n);
	
	printf("Sorting results:");
	for (i=0 ; i<n ; i++)
	{
		printf("%4d",a[i]);
	}
	puts("\n");
	
	return 0;
}

void swap(int *p1,int *p2)
{
	int temp;
	temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}

void BubbleSort(int a[], int n)
{
	int i,j;
	for (i=0 ; i<n-1 ; i++)
	{
		for (j=0 ; j<n-1-i ; j++)
		{
			if (a[j] > a[j+1])
			{
				swap(&a[j],&a[j+1]);
			}
		}
	}
}

3、某小区实行安全管理，分发给业主(共n户，5=<n<=300）出入门卡，为了更好的管理小区内进出人员，
要求搬迁及退租的业主退回门卡，并在数据库内进行删除更新。请编程实现该功能
输入小区业主户数，门卡数据，一个搬迁及退租业主门卡数据，输出删除一个搬迁及退租业主后小区的门卡数据。
删除后的数据顺序按照输入的顺序输出，无需排序调整。

输入数据格式："%d"
输出数据格式："%d "
    当输入迁出门卡数据不存在时 则输出"Error value!"

建议使用给定的函数原型编写并使用函数。
函数原型：
int Del(int a[], int account, int n);
//数组a保存门卡编号数据，account为迁出小区的待删除的门卡数据，n为小区住户数
//成功删除迁出小区门卡数据，函数返回剩余业主户数；若待删除迁出数据不存在时，函数返回-1。
//要求：剩余业主数据在数组中必须按原始输入的业主数据顺序连续存储。

运行样例1：
12↙
4011↙
4032↙
5084↙
5081↙
4031↙
4063↙
6089↙
4153↙
4093↙
5163↙
4181↙
6124↙
4031↙
4011 4032 5084 5081 4063 6089 4153 4093 6124 5163 4181

我的答案：
#include<stdio.h>

int Del(int a[], int account, int n);

int main(int argc,char const*argv[])
{
	int n,i;
	scanf("%d",&n);
	
	int a[n];
	int account;
	int ret;
	
	for (i=0 ; i<n ; i++)
	{
		scanf("%d",&a[i]);
	}
	scanf("%d",&account);
	
	ret = Del(a,account,n);
	if (ret == -1)
	{
		printf("Error value!");
	}
	else
	{
		for (i=0 ; i<n-1 ; i++)
		{
			printf("%d ",a[i]);
		}
	}
	
	return 0;
}

int Del(int a[], int account, int n)
{
	int i,p;
	int flag = 0;
	for (i=0 ; i<n ; i++)
	{
		if (a[i] == account)
		{
			flag = 1;
			p = i;
		}
	}
	if (flag == 0)
	{
		return -1;
	}
	else
	{
		for (i=p ; i<n-1 ; i++)
		{
			a[i] = a[i+1];
		}
		return n-1;
	}
}

总结：
变量定义数组大小先进行初始化
