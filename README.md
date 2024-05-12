#include<stdio.h>
#include<string.h>

//定义一个结构体 
typedef struct  job{
	char name[8];//进程的名字
	int arrivetime;//进程到达时间 
	int runtime;//进程运行时间 
	int cycletime;//进程周转时间 
	int waittime;//进程等待时间 
	int finishtime;//进程完成时间 
	
	 
}job; 


int sjf(struct job jobs[50],int n){
		
			int i,j;
			job tmp;
			
			//先将到达时间从小打到排序
	for(i=0;i<n-1;i++){
		for(j=i+1;j<n;j++){
			if(jobs[i].arrivetime>jobs[j].arrivetime){
				tmp=jobs[i];
				jobs[i]=jobs[j];
				jobs[j]=tmp; 
				
			}
		}	
	}
	
	jobs[0].cycletime=jobs[0].finishtime-jobs[0].arrivetime;
	jobs[0].waittime=jobs[0].cycletime-jobs[0].runtime;
	jobs[0].finishtime=jobs[0].arrivetime+jobs[0].runtime;

		
		//将运行时间从小到大排序 
	for(i=1;i<n-1;i++){
		for(j=i+1;j<n;j++){
			if(jobs[i].runtime>jobs[j].runtime){
				tmp=jobs[i];
				jobs[i]=jobs[j];
				jobs[j]=tmp; 
				
			}
		}	
		//printf(jobs[i].name,jobs[i].runtime);
	}
	
	for(i=1;i<n;i++){
		if(jobs[i-1].finishtime>jobs[i].arrivetime){
			jobs[i].finishtime=jobs[i-1].finishtime+jobs[i].runtime;
			jobs[i].cycletime=jobs[i].finishtime-jobs[i].arrivetime;
			jobs[i].waittime=jobs[i].cycletime-jobs[i].runtime;
			
			
		}else{
			//jobs[i]=jobs[i+1];
			jobs[i+1].finishtime=jobs[i-1].finishtime+jobs[i+1].runtime;
			jobs[i+1].cycletime=jobs[i+1].finishtime-jobs[i+1].arrivetime;
			jobs[i+1].waittime=jobs[i+1].cycletime-jobs[i+1].runtime;
		
			
		}
		
		
	
	 printf("作业名\t到达时间\t运行时间\t周转时间\t等待时间\t完成时间\n");
	for(i=0;i<n;i++){
	
		printf("%s\t   %d\t\t   %d\t\t   %d\t\t   %d\t\t   %d\t\t   ",jobs[i].name,jobs[i].arrivetime,jobs[i].runtime,jobs[i].cycletime,jobs[i].waittime,jobs[i].finishtime);
		printf("\n");
	}
	
	

}



int main(){
	struct job jobs[50];
	int n,i;
	//int tmp;//储存临时变量 
	
	printf("输入进程个数：");
	scanf("%d",&amp;n);
	printf("输入进程的名字，到达时间，运行时间:\n");
	for(i=0;i<n;i++){
		
		scanf("%s",jobs[i].name);//作业名 
		scanf("%d",jobs[i].arrivetime);//到达时间 
		scanf("%d",jobs[i].runtime);//运行时间 
	}
	
	printf("\n");
		printf("进程名\t到达时间\t运行时间\n");
	for(i=0;i<n;i++){
		printf("%s\t   %d\t    %d\n",jobs[i].name,jobs[i].arrivetime,jobs[i].runtime);
	}

	
		printf("短作业优先算法结果：\n");
		sjf(jobs,n);
	
}
