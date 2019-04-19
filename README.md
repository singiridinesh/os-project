 Question 16: -  Design a scheduler that can schedule the processes arriving system at periodicalintervals.
Every process is assigned with a fixed time slice t milliseconds. 
If it is not able tocomplete its execution within the assigned time quantum, then automated timer generates aninterrupt. 
The scheduler will select the next process in the queue and dispatcher dispatches theprocess to processor for execution. 
Compute the total time for which processes were in the queuewaiting for the processor. 
Take the input for CPU burst, arrival time and time quantum from theuser.

code:-

#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
int main()
{
	printf("\n\n\t\t *******WELCOME TO ROUND ROBIN SCHEDULING******* \n");
	int n,n1;
	printf("Enter the number of process \n");
	scanf("%d",&n);
	n1=n;
	int ts;
	printf("\n Enter the Timeslice \n");
	scanf("%d",&ts);
	int pid[50],bt[30];
	int i;
	int need[20];
	for(i=1;i<=n;i++)
	{
		printf("\n Enter the process ID \n");
		scanf("%d",&pid[i]);
		printf("\n Enter the Burst time \n");
		scanf("%d",&bt[i]);
		need[i]=bt[i];
	}
	int flag[30];
	int wt[40];
	for(i=1;i<=n;i++)
	{
	    flag[i]=1;
		wt[i]=0;
	}
	while(n!=0)
	{
		for(i=1;i<=n;i++)
		{
			if(need[i]>=ts)
			{
				for(int j=1;j<=n;j++)
				{
				    if((i!=j)&&(flag[i]==1)&&(need[j]=0))
					wt[j]+=ts;
				}
				need[i]-=ts;
				if(need[i]==0)
				{
					flag[i]=0;
					n--;
				}
			}
			else
			{
				for(int j=1;j<=n;j++)
				{
					if((i!=j)&&(flag[i]==1)&&(need[j]!=0))
					wt[j]+=need[i];
				}
				need[i]=0;
				n--;
				flag[i]=0;
			}
		}
	}
	int tat[40],a=0,b=0;
	for(i=1;i<=n1;i++)
	{
	    tat[i]=wt[i]+bt[i];
		a=a+wt[i];
		b=b+tat[i];
	}
	float awt,atat;
	awt=(float)a/n1;
	atat=(float)b/n1;
	printf("\n\n ******ROUND ROBIN SCHEDULING ALGORITHM****** \n\n");
	printf("\n\n Process \tProcess ID \tBurst time \tWaiting time \tTurnaround \n");
	for(i=1;i<=n1;i++)
	{
		printf("\n %5d \t\t %5d \t\t %5d \t\t %5d \t\t %5d \n",i,pid[i],bt[i],wt[i],tat[i]);
	}
	printf("\n the Average waiting time=4.2f",awt);
	printf("\n the Average turn around time=4.2f",atat);
	getch();
}
