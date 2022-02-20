 Prim's algorithm

#include<stdio.h>
#include<conio.h>
int a,b,u,v,n,i,j,ne=1;
int visited[10]={0},min,mincost=0,cost[10][10];
void main()
{
clrscr();
printf("\nEnter the number of nodes:");
scanf("%d",&n);
printf("\nEnter the adjacency matrix:\n");
for(i=1;i<=n;i++)
for(j=1;j<=n;j++)
{
scanf("%d",&cost[i][j]);
if(cost[i][j]==0)
cost[i][j]=999;
}
visited[1]=1;
printf("\n");
while(ne < n)
{
for(i=1,min=999;i<=n;i++)
for(j=1;j<=n;j++)
if(cost[i][j]< min)
if(visited[i]!=0)
{
min=cost[i][j];
a=u=i;
b=v=j;
}
if(visited[u]==0 || visited[v]==0)
{
printf("\n Edge %d:(%d %d) cost:%d",ne++,a,b,min);
mincost+=min;
visited[b]=1;
}
cost[a][b]=cost[b][a]=999;
}
printf("\n Minimun cost=%d",mincost);
getch();
}









b.DFS method.

#include<stdio.h>
#include<conio.h>
int a[20][20],reach[20],n;
void dfs(int v){
 int i;
 reach[v]=1;
 for(i=1;i<=n;i++)
 if(a[v][i]&&!reach[i]){
 printf(â€œ\n%d->%dâ€,v,i);
 dfs(i);
 }
}
int main(){
 int i,j,count=0;
 printf(â€œ\nEnter no of vertices : â€œ);
 scanf(â€œ%dâ€,&n);
 for(i=1;i<=n;i++)
 for(j=1;j<=n;j++){
 reach[i]=0;
 a[i][j]=0;
 }
 printf(â€œ\nEnter adjacency matrix : \nâ€);
for(i=1;i<=n;i++)
 for(j=1;j<=n;j++)
 scanf(â€œ%dâ€,&a[i][j]);
 dfs(1);
 for(i=1;i<=n;i++)
 if(reach[i])
 count++;
 if(count==n)
 printf(â€œ\nGraph is connected.â€);
 else
 printf(â€œ\nGraph is disconnected.â€);
 getch();
 return(0);
 }










a. BFS method.

#include<stdio.h>
#define size 20
#define true 1
#define false 0
int queue[size],visit[20],rear=-1,front=0;
int n,s,adj[20][20],flag=0;
void insertq(int v)
{
 queue[++rear]=v;
}
int deleteq()
{
 return(queue[front++]);
}
int qempty()
{
 if(rear<front)
 return 1;
 else
 return 0;
}
void bfs(int v)
{
 int w;
 visit[v]=1;
 insertq(v);
 while(!qempty())
 {
 v=deleteq();
 for(w=1;w<=n;w++)
 if((adj[v][w]==1) && (visit[w]==0))
 {
 visit[w]=1;
 flag=1;
 printf("v%d\t",w);
 insertq(w);
}
 }
}
void main()
{
 int v,w;
 printf("Enter the no.of vertices:\n");
 scanf("%d",&n);
 printf("Enter adjacency matrix:");
 for(v=1;v<=n;v++)
 {
 for(w=1;w<=n;w++)
 scanf("%d",&adj[v][w]);
 }
 printf("Enter the start vertex:");
 scanf("%d",&s);
 printf("Reachability of vertex %d\n",s);
 for(v=1;v<=n;v++)
 visit[v]=0;
 bfs(s);
 if(flag==0)
 {
 printf("No path found!!\n");
 }
}
















Kruskal's algorithm

#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
int i,j,k,a,b,u,v,n,ne=1;
int min,mincost=0,cost[9][9],parent[9];
int find(int);
int uni(int,int);
void main()
{
clrscr();
printf("\n Implementation of Kruskal's algorithmnn");
printf("\n Enter the no. of verticesn");
scanf("%d",&n);
printf("\n Enter the cost adjacency matrixn");
for(i=1;i<=n;i++)
{
 for(j=1;j<=n;j++)
 {
 scanf("%d",&cost[i][j]);
 if(cost[i][j]==0)
 cost[i][j]=999;
 }
 parent[i]=i;
}
printf("nThe edges of Minimum Cost Spanning Tree arenn");
while(ne<n)
{
 for(i=1,min=999;i<=n;i++)
 {
 for(j=1;j<=n;j++)
 {
 if(cost[i][j]<min)
 {
 min=cost[i][j];
 a=u=i;
 b=v=j;
 }
 }
 }
 u=find(u);
 v=find(v);
 if(uni(u,v))
 {
printf("n%d edge (%d,%d) =%dn",ne++,a,b,min);
 mincost +=min;
 }
 cost[a][b]=cost[b][a]=999;
}
printf("ntMinimum cost = %dn",mincost);
getch();
}
int find(int i)
{
// while(parent[i])
 i=parent[i];
return i;
}
int uni(int i,int j)
{
if(i!=j)
{
 parent[j]=i;
 return 1;
}
return 0;
}















0/1 Knapsack problem using Dynamic Programming.

#include<iostream.h>
#include<conio.h>
int max(int a, int b)
{ return (a > b)? a : b;
}
void main()
{
int P[5]={0,1,2,5,6} ;
int wt[5]={0,2,3,4,5} ;
int m=8,n=4;
int k[5][9];
for(int i=0;i<=n;i++)
{
 for(int w=0;w<=m;w++)
 {
 if(i==0||w==0)
 k[i][w]=0;
 else if(wt[i]<=w)
 k[i][w]=max(P[i]+k[i-1][w-wt[i]],k[i-1][w]);
 else
 k[i][w]=k[i-1][w];
 }
}
for(i=0;i<=n;i++)
{
cout<<endl;
for(int j=0;j<=m;j++)
{
cout<<k[i][j];
}
}
i=n;int j=m;
while(i>0 && j>0)
{
if(k[i][j]==k[i-1][j])
{
cout<<i<<"=0"<<endl;
i--;
}
else
{
cout<<i<<"=1"<<endl;
j=j-wt[i];i--;
}
}
getch();
}





















 1 : Sort a given set of elements using the Quicksort method and determine the time required to sort the
elements. Repeat the experiment for different values of n, the number of elements in the list to be sorted and plot
a graph of the time taken versus n. The elements can be read from a file or can be generated using the random
number generator.
# include <stdio.h>
# include <conio.h>
# include <time.h>
void Exch(int *p, int *q)
{
int temp = *p;
*p = *q;
*q = temp;
}
void QuickSort(int a[], int low, int high)
{
int i, j, key, k; if(low>=high)
return;
key=low; i=low+1; j=high; while(i<=j)
{
while ( a[i] <= a[key] ) i=i+1; while ( a[j] > a[key] ) j=j-1;
if(i<j) Exch(&a[i], &a[j]);
}
}
void main()
{
Exch(&a[j], &a[key]);
QuickSort(a, low, j-1);
QuickSort(a, j+1, high);
int n, a[1000],k;
clock_t st,et; double ts; clrscr();
printf("\n Enter How many Numbers: "); scanf("%d", &n);
printf("\nThe Random Numbers are:\n");
for(k=1; k<=n; k++)
{
a[k]=rand(); printf("%d\t",a[k]);
}
}
st=clock();
QuickSort(a, 1, n);
et=clock();
ts=(double)(et-st)/CLOCKS_PER_SEC;
printf("\nSorted Numbers are: \n ");
for(k=1; k<=n; k++)
printf("%d\t", a[k]);
printf("\nThe time taken is %e",ts);
getch();
}





















Merge Sort 

#include<stdio.h>
void mergesort(int a[],int i,int j);
void merge(int a[],int i1,int j1,int i2,int j2);
int main()
{
int a[30],n,i;
printf("Enter no of elements:");
scanf("%d",&n);
printf("Enter array elements:");
for(i=0;i<n;i++)
scanf("%d",&a[i]);
mergesort(a,0,n-1);
printf("\nSorted array is :");
for(i=0;i<n;i++)
printf("%d ",a[i]);
return 0;
}
void mergesort(int a[],int i,int j)
{
int mid;
if(i<j)
{
mid=(i+j)/2;
mergesort(a,i,mid); //left recursion
mergesort(a,mid+1,j); //right recursion
merge(a,i,mid,mid+1,j); //merging of two sorted sub-arrays
}
}
void merge(int a[],int i1,int j1,int i2,int j2)
{
int temp[50]; //array used for merging
int i,j,k;
i=i1; //beginning of the first list
j=i2; //beginning of the second list
k=0;
while(i<=j1 && j<=j2) //while elements in both lists
{
if(a[i]<a[j])
temp[k++]=a[i++];
else
temp[k++]=a[j++];
}
while(i<=j1) //copy remaining elements of the first list
temp[k++]=a[i++];
while(j<=j2) //copy remaining elements of the second list
temp[k++]=a[j++];
//Transfer elements from temp[] back to a[]
for(i=i1,j=0;i<=j2;i++,j++)
a[i]=temp[j];
}


















