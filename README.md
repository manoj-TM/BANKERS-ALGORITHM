# BANKERS-ALGORITHM
implementing bankers algorithm in c programme.
#include<stdio.h>

int p,r;
int allo[10][10],max[10][10],avi[10],need[10][10];
int seq[10],count=0;

void calc_func()
{
	int i,j,flag1=1,flag2=0,k;

	while(flag1)
	{
		flag1=0;
		for(i=0;i<p;i++)
		{
			flag2=0;
			for(k=0;k<p;k++)
			{
				if(seq[k]==i)
				{
					flag2=1;
					break;
				}
			}

			if(flag2==1)
				continue;

			for(j=0;j<r;j++)
			{
				if(need[i][j]<=avi[j])
				{
					if(j==r-1)
					{
						seq[count]=i;
						count=count+1;
						flag1=1;
						avi[j-2]=avi[j-2]+allo[i][j-2];
						avi[j-1]=avi[j-1]+allo[i][j-1];
						avi[j]=avi[j]+allo[i][j];
					}
				}
				else
					break;
			}
		}
	}
}

void input_func()
{
	int i,j;

	printf("enter the number of processes: ");
	scanf("%d",&p);
	printf("enter the number of resources: ");
	scanf("%d",&r);

	printf("enter the allocation matrix: \n");
	for(i=0;i<p;i++)
		for(j=0;j<r;j++)
			scanf("%d",&allo[i][j]);

	printf("enter the maximum matrix: \n");
	for(i=0;i<p;i++)
		for(j=0;j<r;j++)
			scanf("%d",&max[i][j]);	

	printf("enter the avilable vector: \n");
	for(i=0;i<r;i++)
		scanf("%d",&avi[i]);

	printf("the need matrix is : \n");
	for(i=0;i<p;i++)
	{
		for(j=0;j<r;j++)
		{
			need[i][j]=max[i][j]-allo[i][j];
			printf("%d\t",need[i][j]);
		}
		printf("\n");
	}

	for(i=0;i<p;i++)
		seq[i]=-1;

}


int main()
{
	int choice=1,i=0;
	printf("BANKERS ALGORITHM\n");
	while(1)
	{
		input_func();
		calc_func();
		if(count==p)
		{
			printf("the safe sequence exists and the sequence is:<  ");
			for(i=0;i<p;i++)
				printf("p%d\t",seq[i]);
			printf(">");
		}
		else
			printf("safe sequence does not exists");
		printf("\nenter your choice:\n1.continue\n2.exit\n");
		scanf("%d",&choice);
		if(choice==2)
			break;
	}
	return 0;
}
