If the headers option is not showing in Postman, you can follow these steps to manually add the necessary headers:

1. **Create a New Request**:
   - Click "New" -> "Request".

2. **Enter the URL**:
   - Set the URL to the appropriate endpoint (e.g., `http://localhost:3000/register`).

3. **Select the Method**:
   - Choose the HTTP method (e.g., `POST`).

4. **Add Headers Manually**:
   - Click on the "Headers" tab.
   - Add a new header:
     - Key: `Content-Type`
     - Value: `application/json`

5. **Set the Body**:
   - Click on the "Body" tab.
   - Select "raw" and then select "JSON" from the dropdown.
   - Enter the JSON data. For example:
     ```json
     {
       "name": "jyotsna",
       "work": "Assistant Professor",
       "password": "abc"
     }
     ```

6. **Send the Request**:
   - Click "Send".

Repeat these steps for each endpoint you want to test. Here is the detailed process for each endpoint:

### Register a User
- **URL**: `http://localhost:3000/register`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "name": "jyotsna",
    "work": "Assistant Professor",
    "password": "abc"
  }
  ```

### Log In a User
- **URL**: `http://localhost:3000/auth`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "name": "jyotsna",
    "password": "abc"
  }
  ```

### Verify Token
- **URL**: `http://localhost:3000/verifyToken`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "token": "your_received_token"
  }
  ```
  9a) Write a shell script to find factorial of a given integer.
echo &quot;Enter a number&quot;
read num
fact=1
while [ $num -gt 1 ]
do
fact=$((fact * num)) #fact = fact * num
num=$((num - 1)) #num = num - 1
done
echo $fact

9 b) Write a C program to create a child process and allow parent to display ‘parent’ and child to display ‘child’.
#include &lt;stdio.h&gt;
#include &lt;unistd.h&gt;
#include &lt;sys/wait.h&gt;
int main(void)
{
int pid;
int status;
pid = fork( );
if(pid &lt; 0)
{
perror(&quot;bad fork&quot;);
exit(1);
}
else if (pid == 0)
{
printf(&quot;I am the child process with id: %d \n&quot;, getpid( ));
}
else if (pid &gt; 0)
{
wait(&amp;status);
printf(&quot;I am the parent process with id: %d \n&quot;, getpid( ));
}
}

9 c) Write a C program in which a parent writes a message to a pipe and the child reads the message
#include&lt;stdio.h&gt;
#include&lt;stdlib.h&gt;
#include&lt;sys/types.h&gt;
#include&lt;unistd.h&gt;
int main()
{
int pfds[2],n;
char buffer[100];
if(pipe(pfds) &lt; 0)
{
perror(&quot;Pipe is not created&quot;);
exit(1);
}
if(fork()&gt;0)
{
printf(&quot;Parent passing value to child\n&quot;);
write(pfds[1],&quot;Hello\n&quot;,6);
wait( );
}
else if (fork()==0)
{
printf(&quot;Child printing received file\n&quot;);
n=read(pfds[0],buffer,100);
write(1,buffer,n);
}
}
////////////////////////////////////////////////////////////////////////////////////////
7. Write C Programs to simulate the following CPU scheduling algorithms:    
a)FCFS              b) Priority

a) FCFS ALGORITHM:

SOURCE CODE:
#include<stdio.h>
void main()
{
int pid[10],bt[10],wt[10],tat[10],n,twt=0,ttat=0,i;
float awt,atat;
printf("Enter no.of processes:");
scanf("%d",&n);
printf("\n Enter burst times:");
for(i=0;i<n;i++)
scanf("%d",&bt[i]);
wt[0]=0;
tat[0]=bt[0];
for(i=1;i<n;i++)
{
wt[i]=tat[i-1];
tat[i]=bt[i]+wt[i];
}
for(i=0;i<n;i++)
{
ttat= ttat+tat[i];
twt=twt+wt[i];
}
printf("\n PID \t BT \t WT \t TAT");
for(i=0;i<n;i++)
printf("\n %d\t%d\t%d\t%d",i+1,bt[i],wt[i],tat[i]);
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\nAvg. Waiting Time=%f",awt);
printf("\nAvg. Turn around time=%f",atat);
}
 Output:




 
b) PRIORITY ALGORITHM:

SOURCE CODE:
#include<stdio.h>
void main()
{
int pid[10],bt[10],pr[10],wt[10],tat[10],n,twt=0,ttat=0,i,j,t;
float awt,atat;
printf("Enter no.of processes:");
scanf("%d",&n);
printf("\n Enter burst times:");
for(i=0;i<n;i++)
scanf("%d",&bt[i]);
printf("\n Enter PID:");
for(i=0;i<n;i++)
scanf("%d",&pid[i]);
printf("\n Enter Priorities:");
for(i=0;i<n;i++)
scanf("%d",&pr[i]);
for(i=0;i<n;i++)
{
for(j=i+1;j<n;j++)
{
if(pr[i]>pr[j])
{
t=pr[i];
pr[i]=pr[j];
pr[j]=t;

t=bt[i];
bt[i]=bt[j];
bt[j]=t;

t=pid[i];
pid[i]=pid[j];
pid[j]=t;
}
}
}
wt[0]=0;
tat[0]=bt[0];
for(i=1;i<n;i++)
{
wt[i]=tat[i-1];
tat[i]=bt[i]+wt[i];
}
for(i=0;i<n;i++)
{
ttat= ttat+tat[i];
twt=twt+wt[i];
}
printf("\n PID PRIORITY \t BT \t WT \t TAT");
for(i=0;i<n;i++)
printf("\n %d\t%d\t%d\t%d\t%d",pid[i],pr[i],bt[i],
wt[i],tat[i]);
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\nAvg. Waiting Time=%f",awt);
printf("\nAvg. Turn around time=%f",atat);
}

Output:
///////////////////////////////////////////////////////////////
Write C Programs to simulate the following CPU scheduling algorithms:    
a)SJF    b) Round Robin

a)SJF  
#include<stdio.h>
void main(){
int pid[10],bt[10],wt[10],tat[10],n,twt=0,ttat=0,i,j,t;
float awt,atat;
printf("Enter no.of processes:");
scanf("%d",&n);
printf("\n Enter burst times:");
for(i=0;i<n;i++)
scanf("%d",&bt[i]);
printf("\n Enter PID:");
for(i=0;i<n;i++)
scanf("%d",&pid[i]);
for(i=0;i<n;i++)
{
for(j=i+1;j<n;j++)
{
if(bt[i]>bt[j])
{
t=bt[i];
bt[i]=bt[j];
bt[j]=t;

t=pid[i];
pid[i]=pid[j];
pid[j]=t;
}}}
wt[0]=0;
tat[0]=bt[0];
for(i=1;i<n;i++)
{
wt[i]=tat[i-1];
tat[i]=bt[i]+wt[i];
}
for(i=0;i<n;i++)
{
ttat= ttat+tat[i];
twt=twt+wt[i];
}
printf("\n PID \t BT \t WT \t TAT");
for(i=0;i<n;i++)
printf("\n %d\t%d\t%d\t%d",pid[i],bt[i],wt[i],tat[i]);
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\nAvg. Waiting Time=%f",awt);
printf("\nAvg. Turn around time=%f",atat);
}

b) Round Robin
#include<stdio.h>
void main()	
{
int ts,bt1[10],wt[10],tat[10],i,j=0,n,bt[10],ttat=0,twt=0,tot=0;
float awt,atat;
printf("Enter the number of Processes \n");
scanf("%d",&n);
printf("\n Enter the Timeslice \n");
scanf("%d",&ts);
printf("\n Enter the Burst Time for the process");
for(i=1;i<=n;i++){
scanf("%d",&bt1[i]);
bt[i]=bt1[i];
}
while(j<n){
for(i=1;i<=n;i++){
if(bt[i]>0){
if(bt[i]>=ts){
tot+=ts;
bt[i]=bt[i]-ts;
if(bt[i]==0){
j++;
tat[i]=tot;
}}
else{
tot+=bt[i];
bt[i]=0;
j++;
tat[i]=tot;
}}}}
for(i=1;i<=n;i++){
wt[i]=tat[i]-bt1[i];
twt=twt+wt[i];
ttat=ttat+tat[i];
}
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\n PID \t BT \t WT \t TAT\n");
for(i=1;i<=n;i++) {
printf("\n %d \t %d \t %d \t %d \t\n",i,bt1[i],wt[i],tat[i]);
}
printf("\n The average Waiting Time=%f",awt);
printf("\n The average Turn around Time=%f",atat);
}


Alternate:
Round Robin
#include<stdio.h>
void main()	
{
int n,i,qt,count=0,temp,sq=0,bt[10],wt[10],tat[10],rem_bt[10];
float awt,atat;
printf("Enter the number of Processes \n");
scanf("%d",&n);
printf("\n Enter the quantum time \n");
scanf("%d",&qt);
printf("\n Enter the Burst Time for the process");
for(i=1;i<=n;i++)
{
scanf("%d",&bt[i]);
rem_bt[i]=bt[i];
}
while(1)
{
for(i=0,count=0;i<=n;i++)
{
temp=qt;
if(rem_bt[i]==0)
{
count++:
continue;
}
if(rem_bt[i]>qt)
rem_bt[i]=rem_bt[i]-qt;
else
if(rem_bt[i]>=0)
{
temp=rem_bt[i];
rem_bt[i]=0;
}
sq=sq+temp;
tat[i]=sq;
}

if(n==count)
break
}
for(i=1;i<=n;i++)
{
wt[i]=tat[i]-bt[i];
twt=twt+wt[i];
ttat=ttat+tat[i];
}
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\n PID \t BT \t WT \t TAT\n");
for(i=1;i<=n;i++) {
printf("\n %d \t %d \t %d \t %d \t\n",i,bt1[i],wt[i],tat[i]);
}
printf("\n The average Waiting Time=%f",awt);
printf("\n The average Turn around Time=%f",atat);
}

a)SJF  
#include<stdio.h>
void main(){
int pid[10],bt[10],wt[10],tat[10],n,twt=0,ttat=0,i,j,t;
float awt,atat;
printf("Enter no.of processes:");
scanf("%d",&n);
printf("\n Enter burst times:");
for(i=0;i<n;i++)
scanf("%d",&bt[i]);
printf("\n Enter PID:");
for(i=0;i<n;i++)
scanf("%d",&pid[i]);
for(i=0;i<n;i++)
{
for(j=i+1;j<n;j++)
{
if(bt[i]>bt[j])
{
t=bt[i];
bt[i]=bt[j];
bt[j]=t;

t=pid[i];
pid[i]=pid[j];
pid[j]=t;
}}}
wt[0]=0;
tat[0]=bt[0];
for(i=1;i<n;i++)
{
wt[i]=tat[i-1];
tat[i]=bt[i]+wt[i];
}
for(i=0;i<n;i++)
{
ttat= ttat+tat[i];
twt=twt+wt[i];
}
printf("\n PID \t BT \t WT \t TAT");
for(i=0;i<n;i++)
printf("\n %d\t%d\t%d\t%d",pid[i],bt[i],wt[i],tat[i]);
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\nAvg. Waiting Time=%f",awt);
printf("\nAvg. Turn around time=%f",atat);
}

b) Round Robin
#include<stdio.h>
void main()	
{
int ts,bt1[10],wt[10],tat[10],i,j=0,n,bt[10],ttat=0,twt=0,tot=0;
float awt,atat;
printf("Enter the number of Processes \n");
scanf("%d",&n);
printf("\n Enter the Timeslice \n");
scanf("%d",&ts);
printf("\n Enter the Burst Time for the process");
for(i=1;i<=n;i++){
scanf("%d",&bt1[i]);
bt[i]=bt1[i];
}
while(j<n){
for(i=1;i<=n;i++){
if(bt[i]>0){
if(bt[i]>=ts){
tot+=ts;
bt[i]=bt[i]-ts;
if(bt[i]==0){
j++;
tat[i]=tot;
}}
else{
tot+=bt[i];
bt[i]=0;
j++;
tat[i]=tot;
}}}}
for(i=1;i<=n;i++){
wt[i]=tat[i]-bt1[i];
twt=twt+wt[i];
ttat=ttat+tat[i];
}
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\n PID \t BT \t WT \t TAT\n");
for(i=1;i<=n;i++) {
printf("\n %d \t %d \t %d \t %d \t\n",i,bt1[i],wt[i],tat[i]);
}
printf("\n The average Waiting Time=%f",awt);
printf("\n The average Turn around Time=%f",atat);
}


Alternate:
Round Robin
#include<stdio.h>
void main()	
{
int n,i,qt,count=0,temp,sq=0,bt[10],wt[10],tat[10],rem_bt[10];
float awt,atat;
printf("Enter the number of Processes \n");
scanf("%d",&n);
printf("\n Enter the quantum time \n");
scanf("%d",&qt);
printf("\n Enter the Burst Time for the process");
for(i=1;i<=n;i++)
{
scanf("%d",&bt[i]);
rem_bt[i]=bt[i];
}
while(1)
{
for(i=0,count=0;i<=n;i++)
{
temp=qt;
if(rem_bt[i]==0)
{
count++:
continue;
}
if(rem_bt[i]>qt)
rem_bt[i]=rem_bt[i]-qt;
else
if(rem_bt[i]>=0)
{
temp=rem_bt[i];
rem_bt[i]=0;
}
sq=sq+temp;
tat[i]=sq;
}

if(n==count)
break
}
for(i=1;i<=n;i++)
{
wt[i]=tat[i]-bt[i];
twt=twt+wt[i];
ttat=ttat+tat[i];
}
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\n PID \t BT \t WT \t TAT\n");
for(i=1;i<=n;i++) {
printf("\n %d \t %d \t %d \t %d \t\n",i,bt1[i],wt[i],tat[i]);
}
printf("\n The average Waiting Time=%f",awt);
printf("\n The average Turn around Time=%f",atat);
}


11. Write C Programs SJF RR.txt
Page 2 of 2
Experiment 11
Sarika Sabavath
•
Apr 29

11. Write C Programs SJF RR.txt

///////////Text
Write C programs to simulate the following Fileallocation strategies
a)	Sequential 		b)Linked 	c)Indexed


a)	Sequential 
#include<stdio.h>
main()
{
int n,i,j,b[20],sb[20],t[20],x,c[20][20];
printf("Enter no.of files:");
scanf("%d",&n);
for(i=0;i<n;i++)
{
printf("Enter no. of blocks occupied by file%d",i+1);
scanf("%d",&b[i]);
printf("Enter the starting block of file%d",i+1);
scanf("%d",&sb[i]);
t[i]=sb[i];
for(j=0;j<b[i];j++)
c[i][j]=sb[i]++;
}
printf("Filename\tStart block\tlength\n");
for(i=0;i<n;i++)
printf("%d\t %d \t%d\n",i+1,t[i],b[i]);
printf("Enter file name:");
scanf("%d",&x);
printf("\nFile name is:%d",x);
printf("\nlength is:%d",b[x-1]);
printf("\nblocks occupied:");
for(i=0;i<b[x-1];i++)
printf("%4d",c[x-1][i]);
}



b)Linked
#include<stdio.h>
struct file
{
char fname[10];
int start,size,block[10];
}f[10];
main()
{
int i,j,n;
printf("Enter no. of files:");
scanf("%d",&n);
for(i=0;i<n;i++){
printf("Enter file name:");
scanf("%s",&f[i].fname);
printf("Enter starting block:");
scanf("%d",&f[i].start);
f[i].block[0]=f[i].start;
printf("Enter no.of blocks:");
scanf("%d",&f[i].size);
printf("Enter block numbers:");
for(j=1;j<f[i].size;j++){
scanf("%d",&f[i].block[j]);
}}
printf("File\tstart\tsize\tblock\n");
for(i=0;i<n;i++){
printf("%s\t%d\t%d\t",f[i].fname,f[i].start,f[i].size);
for(j=0;j<f[i].size-1;j++)
printf("%d--->",f[i].block[j]);
printf("%d\n",f[i].block[j]);
}}



c)Indexed

#include<stdio.h>
main()
{
int n,m[20],i,j,sb[20],b[20][20],x;
printf("\nEnter no. of files:");
scanf("%d",&n);
for(i=0;i<n;i++)
{
printf("\nEnter index block of file%d:",i+1);
scanf("%d",&sb[i]);
printf("\nEnter length of file%d:",i+1);
scanf("%d",&m[i]);
printf("enter blocks of file%d:",i+1);
for(j=0;j<m[i];j++)
scanf("%d",&b[i][j]);
}
printf("\nFile\t Index\tLength\n");
for(i=0;i<n;i++)
{
printf("%d\t%d\t%d\n",i+1,sb[i],m[i]);
}
printf("\nEnter file name:");
scanf("%d",&x);
printf("\nfile name is:%d",x);
printf("\nIndex is:%d",sb[x-1]);
printf("\nBlocks occupied are:");
for(j=0;j<m[x-1];j++)
printf("%4d",b[x-1][j]);
}


Write C Programs to simulate the following CPU scheduling algorithms:    
a)SJF    b) Round Robin

a)SJF  
#include<stdio.h>
void main(){
int pid[10],bt[10],wt[10],tat[10],n,twt=0,ttat=0,i,j,t;
float awt,atat;
printf("Enter no.of processes:");
scanf("%d",&n);
printf("\n Enter burst times:");
for(i=0;i<n;i++)
scanf("%d",&bt[i]);
printf("\n Enter PID:");
for(i=0;i<n;i++)
scanf("%d",&pid[i]);
for(i=0;i<n;i++)
{
for(j=i+1;j<n;j++)
{
if(bt[i]>bt[j])
{
t=bt[i];
bt[i]=bt[j];
bt[j]=t;

t=pid[i];
pid[i]=pid[j];
pid[j]=t;
}}}
wt[0]=0;
tat[0]=bt[0];
for(i=1;i<n;i++)
{
wt[i]=tat[i-1];
tat[i]=bt[i]+wt[i];
}
for(i=0;i<n;i++)
{
ttat= ttat+tat[i];
twt=twt+wt[i];
}
printf("\n PID \t BT \t WT \t TAT");
for(i=0;i<n;i++)
printf("\n %d\t%d\t%d\t%d",pid[i],bt[i],wt[i],tat[i]);
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\nAvg. Waiting Time=%f",awt);
printf("\nAvg. Turn around time=%f",atat);
}

b) Round Robin
#include<stdio.h>
void main()	
{
int ts,bt1[10],wt[10],tat[10],i,j=0,n,bt[10],ttat=0,twt=0,tot=0;
float awt,atat;
printf("Enter the number of Processes \n");
scanf("%d",&n);
printf("\n Enter the Timeslice \n");
scanf("%d",&ts);
printf("\n Enter the Burst Time for the process");
for(i=1;i<=n;i++){
scanf("%d",&bt1[i]);
bt[i]=bt1[i];
}
while(j<n){
for(i=1;i<=n;i++){
if(bt[i]>0){
if(bt[i]>=ts){
tot+=ts;
bt[i]=bt[i]-ts;
if(bt[i]==0){
j++;
tat[i]=tot;
}}
else{
tot+=bt[i];
bt[i]=0;
j++;
tat[i]=tot;
}}}}
for(i=1;i<=n;i++){
wt[i]=tat[i]-bt1[i];
twt=twt+wt[i];
ttat=ttat+tat[i];
}
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\n PID \t BT \t WT \t TAT\n");
for(i=1;i<=n;i++) {
printf("\n %d \t %d \t %d \t %d \t\n",i,bt1[i],wt[i],tat[i]);
}
printf("\n The average Waiting Time=%f",awt);
printf("\n The average Turn around Time=%f",atat);
}


Alternate:
Round Robin
#include<stdio.h>
void main()	
{
int n,i,qt,count=0,temp,sq=0,bt[10],wt[10],tat[10],rem_bt[10];
float awt,atat;
printf("Enter the number of Processes \n");
scanf("%d",&n);
printf("\n Enter the quantum time \n");
scanf("%d",&qt);
printf("\n Enter the Burst Time for the process");
for(i=1;i<=n;i++)
{
scanf("%d",&bt[i]);
rem_bt[i]=bt[i];
}
while(1)
{
for(i=0,count=0;i<=n;i++)
{
temp=qt;
if(rem_bt[i]==0)
{
count++:
continue;
}
if(rem_bt[i]>qt)
rem_bt[i]=rem_bt[i]-qt;
else
if(rem_bt[i]>=0)
{
temp=rem_bt[i];
rem_bt[i]=0;
}
sq=sq+temp;
tat[i]=sq;
}

if(n==count)
break
}
for(i=1;i<=n;i++)
{
wt[i]=tat[i]-bt[i];
twt=twt+wt[i];
ttat=ttat+tat[i];
}
awt=(float)twt/n;
atat=(float)ttat/n;
printf("\n PID \t BT \t WT \t TAT\n");
for(i=1;i<=n;i++) {
printf("\n %d \t %d \t %d \t %d \t\n",i,bt1[i],wt[i],tat[i]);
}
printf("\n The average Waiting Time=%f",awt);
printf("\n The average Turn around Time=%f",atat);
}

#include<stdio.h>
int main()
{
    int i,j,n,a[50],frame[10],fno,k,avail,pagefault=0;
    printf("\nEnter the number of Frames : ");
    scanf("%d",&fno);
    printf("\nEnter number of reference string :");
    scanf("%d",&n);
    printf("\n Enter the Reference string :\n");
    for(i=0;i<n;i++)
        scanf("%d",&a[i]);
    for(i=0;i<fno;i++)
        frame[i]= -1;
    j=0;
    printf("\nFIFO PAGE REPLACEMENT ALGORITHM\n\nThe given reference string is:\n\n");
    for(i=0;i<n;i++)
    {
        printf(" %d ",a[i]);
    }
    printf("\n");
    for(i=0;i<n;i++)
    {
        printf("\nReference No %d-> ",a[i]);
        avail=0;
        for(k=0;k<fno;k++)
            if(frame[k]==a[i])
                    avail=1;
        if (avail==0)
        {
            frame[j]=a[i];
            j = (j+1) % fno;
            pagefault++;
            for(k=0;k<fno;k++)
                if(frame[k]!=-1)
                    printf(" %2d",frame[k]);
        }
        printf("\n");
    }
    printf("\nPage Fault Is %d",pagefault);
    return 0;
}





Class comments



By following these steps, you should be able to manually set the headers and validate your API endpoints using Postman.
# fswd
