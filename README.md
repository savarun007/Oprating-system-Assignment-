# Oprating-system-Assignment-
Problem :-
1)	There are 3 student processes and 1 teacher process. Students are supposed to do their assignments and they need 3 things for that pen, paper and question paper. The teacher has an infinite supply of all the three things. One students has pen,an other has paper and another has question paper. The teacher places two things on a shared table and the student having the third complementary thing makes the assignment and tells the teacher on completion. The teacher then places another two things out of the three and again the student having the third thing makes the assignment and tells the teacher on completion. This cycle continues. WAP to synchronize the teacher and the students. 



Explanation:	For the solution on this problem i have take 2d array of all the student processer and resources and initialized that array with 0. Then for the continuty i have made 3 different student processed in 3 different function named stud1,stud2,stud3 . which is being executed by single s_thread and one t_thread for execution of teacher process.	User will get a menu to select any two out of three resources that are to be placed on shared table.	If one process is completed there will be a message printed on the screen saying process is completed.	When one process is executing no other student or teacher process will execute and for achieving this I have used Mutex lock.When a process starts to execute it acquires the lock and when it completes the execution releases the lock.	After completion of all the three processes the program will end.


code 

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
#include<stdbool.h>
int stud[3][4]={0};
void *teacher();
void *stud1();
void *stud2();
void *stud3();
pthread_mutex_t lck;
int ch1,ch2;
int r1,r2;

int main()
{	
printf("\t\t\t---Welcome---\n");
	pthread_mutex_init(&lck,NULL);\
stud[1][1]=1;
	stud[2][2]=2;stud[3][3]=1;
	pthread_t t_thread;
	pthread_t s_thread;
printf("Resources Menu: \n\t\tPress '1' for pen\n\t\tPress '2' for paper \n\t\tPress '3' for   question_paper \n"); 	
	while(1)
{
if(stud[1][4]==1 && stud[2][4]==1 && stud[3][4]==1){break;}
pthread_create(&t_thread, NULL, teacher, NULL);
pthread_join(t_thread,NULL);
	    
if((ch1==1 && ch2==2 || ch2==1 && ch1==2 ) && stud[3][4]==0)
{
	pthread_create(&s_thread, NULL, stud3, NULL);
	pthread_join(s_thread,NULL);
}
else if((ch1==1 && ch2==3 || ch2==1 && ch1==3 ) && stud[2][4]==0)
{
pthread_create(&s_thread, NULL, stud2, NULL);
	pthread_join(s_thread,NULL);
}
else if((ch1==2 && ch2==3 || ch2==2 && ch1==3 ) && stud[1][4]==0)
{
	pthread_create(&s_thread, NULL, stud1, NULL);
pthread_join(s_thread,NULL);
}
else
{
	printf("\n\tError (007): try again.. with different choices.\n");
}
}
printf("\n\t----Done---\n");
}


void *teacher()
{
pthread_mutex_lock(&lck);
	printf("\nFirst Resource on shared tabel:-\t");
	scanf("%d",&ch1);
	printf("Second Resource on shared tabel:-\t");
	scanf("%d",&ch2);
	pthread_mutex_unlock(&lck);
}

void *stud2()
{	
	pthread_mutex_lock(&lck);
	printf("\nChoices Made = 'pen', 'question_paper'\n");
	student[2][4]=1;
	printf("\n\tStudent 2 has Completed the assignment. \n");
	pthread_mutex_unlock(&lck);
}

void *stud3()
{	
	pthread_mutex_lock(&lck);
	printf("\nChoices Made = 'pen', 'paper'\n");
	student[3][4]=1;
	printf("\n\tStudent 3 has Completed the assignment.\n");
	pthread_mutex_unlock(&lck);
}

void *stud1()
{	
	pthread_mutex_lock(&lck);
	printf("\nChoices Made = 'paper', 'question_paper'\n");
	student[1][4]=1;
	printf("\n\tStudent 1 has Completed the assignment.\n");	
	pthread_mutex_unlock(&lck);
}
