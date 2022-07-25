1.3 PROGRAM CODE:
#include<stdio.h>
#include<ctype.h>
#include<conio.h>
#include<process.h>
int main()
{
int a, b, c;
clrscr();
printf("Enter three sides of the triangle");
scanf("%d%d%d", &a, &b, &c);
if((a > 10) || (b > 10) || (c > 10))
{
printf("Out of range");
getch();
exit(0);
}
if((a<b+c)&&(b<a+c)&&(c<a+b))
{
if((a==b)&&(b==c))
{
printf("Equilateral triangle");
}
else if((a!=b)&&(a!=c)&&(b!=c))
{
printf("Scalene triangle");
}
else
printf("Isosceles triangle");
}
else
{
printf("triangle cannot be formed");
}
getch();
return 0;
}


2.3 PROGRAM CODE:
#include<stdio.h>
#include<conio.h>
int main()
{
int locks, stocks, barrels, t_sales, flag = 0;
float commission;
clrscr();
printf("Enter the total number of locks");
scanf("%d",&locks);
if ((locks <= 0) || (locks > 70))
{
flag = 1;
}
printf("Enter the total number of stocks");
scanf("%d",&stocks);
if ((stocks <= 0) || (stocks > 80))
{
flag = 1;
}
printf("Enter the total number of barrelss");
scanf("%d",&barrels);
if ((barrels <= 0) || (barrels > 90))
{
flag = 1;
}
if (flag == 1)
{
printf("invalid input");
getch();
exit(0);
}
t_sales = (locks * 45) + (stocks * 30) + (barrels * 25);
if (t_sales <= 1000)
{
commission = 0.10 * t_sales;
}
else if (t_sales < 1800)
{
commission = 0.10 * 1000;
commission = commission + (0.15 * (t_sales - 1000));
}
else
{
commission = 0.10 * 1000;
commission = commission + (0.15 * 800);
commission = commission + (0.20 * (t_sales - 1800));
}
printf("The total sales is %d \n The commission is %f",t_sales, commission);
getch();
return;
}


3.3 PROGRAM CODE:
#include<stdio.h>
#include<conio.h>
main( )
{
int
month[12]={31,28,31,30,31,30,31,31,30,31,30,31};
int d,m,y,nd,nm,ny,ndays;
clrscr( );
printf("enter the date,month,year");
scanf("%d%d%d",&d,&m,&y);
ndays=month[m-1];
if(y<=1812 || y>2012)
{
printf("Invalid Input Year");
exit(0);
}
if(d<=0 || d>ndays)
{
printf("Invalid Input Day");
exit(0);
}
if(m<1 || m>12)
{
printf("Invalid Input Month");
exit(0);
}
if(m==2)
{
if(y%100==0)
{
if(y%400==0)
ndays=29;
}
else
if(y%4==0)
ndays=29;
}
nd=d+1;
nm=m;
ny=y;
if(nd>ndays)
{
nd=1;
nm++;
}
if(nm>12)
{
nm=1;
ny++;
}
printf("\n Given date is %d:%d:%d",d,m,y);
printf("\n Next day’s date is %d:%d:%d",nd,nm,ny);
getch( );
}



10.3. Code
1. #include<stdio.h>
2. #include<conio.h>
3. #include<process.h>
4. void main()
5. {
6. int a[20],n,low = 0,high,mid,key,I,flag = 0;
7. clrscr();
8. printf("Enter the value of n:\n");
9. scanf("%d",&n);
10 printf("Enter the elements in ASCENDING order\n");
11. for(i=0;i<n;i++)
12. {
13. scanf("%d",&a[i]);
14. }
15. printf("Enter the key element to be searched\n");
16. scanf("%d",&key);
17 high=n-1;
18 while(low<=high)
19. {
20. mid=(low+high)/2;
21. if(a[mid]==key)
22. {
23. printf("Successful search\n");
24. printf("Element found at Location %d\n",mid+1);
25. flag = 1;
26. break;
27. }
28. else if(a[mid]<key)
29. {
30. low=mid+1;
31. }
32. else
33. {
34. high=mid-1;
35. }
36. }
37. if (flag == 1)
38. printf("Key Element found\n");
39. else
40. printf(“Key Element not found\n”)
41. }


11.3. CODE
1. #include <stdio.h>
2. int partition (int arr[], int l, int h);
3. void quicksort(int arr[], int l, int h);
4. int main()
5. {
6. int arr[20],n,i;
7. clrscr();
8. printf("Enter the size of the array");
9. scanf("%d",&n);
10. if (n <= 0)
11 {
12. printf(“Number of elements cannot be zero”); getch();
13. }
14. else
15. {
16. printf("Enter %d elements",n);
17. for(i=0;i<n;i++)
18. scanf("%d",&arr[i]);
19. quickSort( arr, 0, n - 1 );
20. printf("Elements of the array are;");
21. for(i=0;i<n;i++)
22. printf("%d",arr[i]);
23. getch();
24. return 0;
25. }
26. }
27. void quickSort (int arr[], int l, int h)
28. { 
29. int stack[10],p;
30. int top = -1;
31. stack[ ++top ] = l;
32. stack[ ++top ] = h;
33. while ( top >= 0 )
34. {
35. h = stack[ top-- ];
36. l = stack[ top-- ];
37. p = partition( arr, l, h );
38. if ( p-1 > l )
39.{
40. stack[ ++top ] = l;
41. stack[ ++top ] = p - 1;
42.}
43. if ( p+1 < h )
44.{
45. stack[ ++top ] = p + 1;
46. stack[ ++top ] = h;
47.}
48. }
49.}
50. int partition (int arr[], int l, int h)
51.{
52. int x = arr[h], t;
53. int i = (l - 1), j;
54. for (j = l; j <= h- 1; j++) 
55. {
56. if (arr[j] <= x)
57. {
58. i++;
59. t = arr[i];
60. arr[i] = arr[j];
61. arr[j] = t; 
62. }
63. }
64. t = arr[i+1];
65. arr[i+1] = arr[h];
66. arr[h] = t;
67. return (i + 1);
68. }



12.3 PROGRAM CODE:
#include<stdio.h>
main()
{
float kan,eng,hindi,maths,science, sst,avmar;
printf("Letter Grading\n");
printf("SSLC Marks Grading\n");
printf("Enter the marks for Kannada:");
scanf("%f",&kan);
printf("enter the marks for English:");
scanf("%f",&eng);
printf("enter the marks for Hindi:");
scanf("%f",&hindi);
printf("enter the marks for Maths");
scanf("%f",&maths);
printf("enter the marks for Science:");
scanf("%f",&science);
printf("enter the marks for Social Science:");
scanf("%f",&sst);
avmar=(kan+eng+hindi+maths+science+sst)/6.25;
printf("the average marks are=%f\n",avmar);
if((avmar<35)&&(avmar>0))
printf("fail");
else 
if((avmar<=40)&&(avmar>35))
printf("Grade C");
else 
if((avmar<=50)&&(avmar>40))
printf("Grade C+");
else 
if((avmar<=60)&&(avmar>50))
printf("Grade B");
else 
if((avmar<=70)&&(avmar>60))
printf("Grade B+");
else 
if((avmar<=80)&&(avmar>70))
printf("Grade A");
else 
if((avmar<=100)&&(avmar>80))
printf("Grade A+");
}
