# Calculating-Moving-Average-in-C

Simple program - that reads an external file containing the close of a certain stock, and compares one trade at a time from last 15 days to now and determines if the stock is moving up and tells me the percentage.

A sample data file of only the closing price is 

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


Code that reads the file and compares line by line

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
