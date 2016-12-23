//# Yihao-GUO-s-home
//the code, program, some tips, other things that I want to learn
#include<iostream>
#include<cstring>
using namespace std;
//直接插入排序
void InsertSort(int r[], int n) //升序排列 
{
	for (int i = 2; i <= n; i++)  //i从2~n循环，共n-1趟排序
	{
		r[0] = r[i];
		int j = i - 1;
		for (; r[0]<r[j]; j--)
			r[j + 1] = r[j];
		r[j + 1] = r[0];
	}
	for (int k = 1;k <= n;k++)
		cout << r[k] << ' ';
}
//希尔排序
void ShellInsert(int r[], int n)
{
	for (int d = n / 2; d >= 1;d = d / 2) //以d为增量
	{
		for (int i = d + 1;i <= n; i++)  //一趟希尔排序
		{
			if (r[i] < r[i - d])
			{
				r[0] = r[i];
				int j = i - d;
				for (; j>0 && r[0]<r[j]; j = j - d)
					r[j + d] = r[j];
				r[j + d] = r[0];
			}
		}
	}
	for (int k = 1;k <= n;k++)
		cout << r[k] << ' ';
}
//起泡排序
void BubbleSort(int r[], int n)
{
	int pos = n;
	while (pos != 0)
	{
		int bound = pos;  //本次无序记录的范围
		pos = 0;
		for (int i = 1;i<bound; i++)
			if (r[i] > r[i + 1])// 相邻记录比较
			{
				r[0] = r[i];r[i] = r[i + 1];   r[i + 1] = r[0];
				pos = i;                                        //交换				pos = i;
			}
	}
	for (int k = 1;k <= n;k++)
		cout << r[k] << ' ';
}
//快速排序
int Partion(int r[], int first, int end)
{
	int i = first; int j = end;
	int pivot = r[i];  //选取基准记录
	while (i<j)
	{
		while ((i<j) && (r[j] >= pivot))//右侧扫描
			j--;
		r[i] = r[j];
		while ((i<j) && (r[i] <= pivot)) //左侧扫描
			i++;
		r[j] = r[i];
	}
	r[i] = pivot;
		return i;
}
void Qsort(int r[], int i, int j)
{
	if (i<j)
	{
		int pivotloc = Partion(r, i, j);
		Qsort(r, i, pivotloc - 1);
		Qsort(r, pivotloc + 1, j);
	}
}
//简单选择排序
void SelectSort(int r[], int n)
{
	for (int i = 1; i<n; i++)  //n-1趟排序
	{
		int index = i;	//假设index是最小的 
		for (int j = i + 1; j <= n; j++)	//查找最小记录的位置 
			if (r[j] < r[index])
				index = j;
		if (index != i)	//若第一个就是最小元素，则不用交换 
		{
			r[0] = r[i];
			r[i] = r[index];
			r[index] = r[0];	//利用r[0]作为临时空间交换记录
		}
	}
	for (int k = 1;k <= n;k++)
		cout << r[k] << ' ';
}
//堆排序
void Sift(int r[], int k, int m)
{
	int i = k;
	int j = 2 * k;
	while (j <= m)
	{
		if (j < m&&r[j] < r[j + 1])
			j++;
		if (r[j] <= r[i])
			break;
		else
		{
			r[0] = r[j];
			r[j] = r[i];
			r[i] = r[0];
		}
		i = j;
		
	}
}
void Heapsort(int r[], int n)
{
	for (int i = n / 2;i >= 1;i--)
	{
		Sift(r, i, n);
	}
	for (int i = n;i > 1;i--)
	{
		r[0] = r[1];
		r[1] = r[i];
		r[i] = r[0];
		Sift(r, 1, i - 1);
	}
	for (int k = 1;k <= n;k++)
		cout << r[k] << ' ';
}

int main()
{
	int i = 1;
	while (i)
	{
		//初始化三种数组
		cout << " 请输入序列长度：n=";
		int n;
		cin >> n;
		int *a = new int[n + 1]; a[0] = 0;
		int *b = new int[n + 1]; b[0] = 0;
		int *c = new int[n + 1]; c[0] = 0;
		//对于正序数组
		cout << "请输入长度为n的正序序列:" << endl;
		for (int i = 1;i <= n;i++)
		{
			cin >> a[i];
		}
		cout << "对于该正序序列" << endl;
		cout << "其直接插入排序为：" << endl;
			int *a1 = new int[n + 1];
		memcpy(a1, a, (n + 1) * sizeof(int));
		InsertSort(a1, n);
		cout << endl << "其希尔排序为：" << endl;
		delete[]a1;
		int *a2 = new int[n + 1];
		memcpy(a2, a, (n + 1) * sizeof(int));
		ShellInsert(a2, n);
		delete[]a2;
		cout << endl << "其起泡排序为：" << endl;
		int *a3 = new int[n + 1];
		memcpy(a3, a, (n + 1) * sizeof(int));
		BubbleSort(a3, n);
		delete[]a3;
		cout << endl << "其快速排序为：" << endl;
		int *a4 = new int[n + 1];
		memcpy(a4, a, (n + 1) * sizeof(int));
		Qsort(a4, 1,n);
		for(int i=1;i<=n;i++)
		{
			cout << a4[i] << ' ';
		}
		delete[]a4;
		cout << endl << "其简单选择排序为：" << endl;
		int *a5 = new int[n + 1];
		memcpy(a5, a, (n + 1) * sizeof(int));
		SelectSort(a5, n);
		delete[]a5;
		cout << endl << "其堆排序为：" << endl;
		int *a6 = new int[n + 1];
		memcpy(a6, a, (n + 1) * sizeof(int));
		Heapsort(a6, n);
		delete[]a6;
		cout << endl;
		//对于逆序数组
		cout << "请输入长度为n的逆序序列:" << endl;
		for (int i = 1;i <= n;i++)
		{
			cin >> b[i];
		}
		cout << "对于该逆序序列" << endl;
		cout << "其直接插入排序为：" << endl;
		int *b1 = new int[n + 1];
		memcpy(b1, b, (n + 1) * sizeof(int));
		InsertSort(b1, n);
		cout << endl << "其希尔排序为：" << endl;
		delete[]b1;
		int *b2 = new int[n + 1];
		memcpy(b2, b, (n + 1) * sizeof(int));
		ShellInsert(b2, n);
		delete[]b2;
		cout << endl << "其起泡排序为：" << endl;
		int *b3 = new int[n + 1];
		memcpy(b3, b, (n + 1) * sizeof(int));
		BubbleSort(b3, n);
		delete[]b3;
		cout << endl << "其快速排序为：" << endl;
		int *b4 = new int[n + 1];
		memcpy(b4, b, (n + 1) * sizeof(int));
		Qsort(b4, 1, n);
		for (int i = 1;i <= n;i++)
		{
			cout << b4[i] << ' ';
		}
		delete[]b4;
		cout << endl << "其简单选择排序为：" << endl;
		int *b5 = new int[n + 1];
		memcpy(b5, b, (n + 1) * sizeof(int));
		SelectSort(b5, n);
		delete[]b5;
		cout << endl << "其堆排序为：" << endl;
		int *b6 = new int[n + 1];
		memcpy(b6, b, (n + 1) * sizeof(int));
		Heapsort(b6, n);
		delete[]b6;
		cout << endl;
		//对于乱序序列
		cout << "请输入长度为n的乱序序列:" << endl;
		for (int i = 1;i <= n;i++)
		{
			cin >> c[i];
		}
		cout << "对于该乱序序列" << endl;
		cout << "其直接插入排序为：" << endl;
		int *c1 = new int[n + 1];
		memcpy(c1, c, (n + 1) * sizeof(int));
		InsertSort(c1, n);
		cout << endl << "其希尔排序为：" << endl;
		delete[]c1;
		int *c2 = new int[n + 1];
		memcpy(c2, c, (n + 1) * sizeof(int));
		ShellInsert(c2, n);
		delete[]c2;
		cout << endl << "其起泡排序为：" << endl;
		int *c3 = new int[n + 1];
		memcpy(c3, c, (n + 1) * sizeof(int));
		BubbleSort(c3, n);
		delete[]c3;
		cout << endl << "其快速排序为：" << endl;
		int *c4 = new int[n + 1];
		memcpy(c4, c, (n + 1) * sizeof(int));
		Qsort(c4, 1, n);
		for (int i = 1;i <= n;i++)
		{
			cout << c4[i] << ' ';
		}
		delete[]c4;
		cout << endl << "其简单选择排序为：" << endl;
		int *c5 = new int[n + 1];
		memcpy(c5, c, (n + 1) * sizeof(int));
		SelectSort(c5, n);
		delete[]c5;
		cout << endl << "其堆排序为：" << endl;
		int *c6 = new int[n + 1];
		memcpy(c6, c, (n + 1) * sizeof(int));
		Heapsort(c6, n);
		delete[]c6;
		cout << endl;
		cout << "是否继续（继续：1，终止：0）：";
		cin >> i;
	}
}
