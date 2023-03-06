# Calculating-Percentage_a_Stock moved in 15 days. C Program

Simple program - that reads an external file containing the close of a certain stock, and compares one trade at a time from last 15 days to now and determines if the stock is moving up and tells me the percentage.

## A sample data file of only the closing price for last 15 days is :

https://www.investopedia.com/terms/m/movingaverage.asp

## Method 1: Below is a sample using one close over the next day

```
159.195938
159.595001
161.949997
163.809998
166.750000
165.889999
165.509995
168.240005
165.179993
164.699997
165.490005
167.809998
171.000000
167.800003
164.929993

```


## Code that reads the file and compares line by line

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main ( ) {

	int step;
	FILE *fptr;
	char str[200];
	int list[100];
	
	fptr = fopen("adjclose.dat","r");
	
	if(fptr == NULL)
	{
	   printf("Error!");   
	   exit(1);             
	}
	int count = 0;
	while( fgets (str, 200, fptr)!=NULL ) {
	   /* writing content to stdout */
	   //puts(str);
	   list[count] = atoi(str);
	   count++;
	}
	printf ("lines are %d\n", count);
	
	for ( int i=0; i<count; i++ ) {
	   printf ("%d\n", (list[i]));
	}
        int moving_avg=0;
	int ref=0;
	for ( int i=0; i<count; i++ ) {
 	   ref = list[i];
  	   printf (" %d) ref = %d  list[i+1] = %d,  moving-avg %d\n", i, ref, list[i+1], moving_avg );

	   if ( ref < list[i+1]) {
		moving_avg++;
	   }
           ref= list[i+1];
	}
	printf (" Percentage = %.2f\n", (float)moving_avg/ (float)count * 100 );
		   
		
	fclose(fptr);
	return 1;

}

```


## Output - Note the percentage in the last line- that tells stock moved 50% of the time.

```
lines are 15
159
159
161
163
166
165
165
168
165
164
165
167
171
167
164
 0) ref = 159  list[i+1] = 159,  moving-avg 0
 1) ref = 159  list[i+1] = 161,  moving-avg 0
 2) ref = 161  list[i+1] = 163,  moving-avg 1
 3) ref = 163  list[i+1] = 166,  moving-avg 2
 4) ref = 166  list[i+1] = 165,  moving-avg 3
 5) ref = 165  list[i+1] = 165,  moving-avg 3
 6) ref = 165  list[i+1] = 168,  moving-avg 3
 7) ref = 168  list[i+1] = 165,  moving-avg 4
 8) ref = 165  list[i+1] = 164,  moving-avg 4
 9) ref = 164  list[i+1] = 165,  moving-avg 4
 10) ref = 165  list[i+1] = 167,  moving-avg 5
 11) ref = 167  list[i+1] = 171,  moving-avg 6
 12) ref = 171  list[i+1] = 167,  moving-avg 7
 13) ref = 167  list[i+1] = 164,  moving-avg 7
 14) ref = 164  list[i+1] = 0,  moving-avg 7
 Percentage = 46.67
 
 
 ```


## Method Two:


Calculate the mean of the closing prices.


