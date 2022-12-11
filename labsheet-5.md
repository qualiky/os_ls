# Labsheet 4: Using the visual editor in UNIX

___

## Objectives

1. To understand the basics of environment variable in UNIX systems.
2. To pass arguments to programs

## Theory  
  
An editor is the program that is used to edit source code. There are many text editors available for Linux, but the two most widely used are Visual Editor Improved (VIM) and Emacs. Other example includes, nano, elvis, vile, etc. 

## Activity

1. factorialcalc.c

        #include<stdio.h>
        #include<stdlib.h>


        int main(){
            int num, prod = 1;
            printf("Enter a number:");
            scanf("%d", &num);
            
            for(int i=1; i<=num; ++i){
                prod *= i;
                printf("At this point, multiplied by %d, product is %d\n", i, prod);
            }

            printf("The factorial is %d\n", prod);
            return 0;
        }

2. patternprinter.c

        #include<stdio.h>

        int main(){
            
            for(int i=0; i<5; ++i) {
                for(int j=0; j<i; ++j){
                    printf("*");
                }
                printf("\n");
            }

            return 0;

        }

3. secondlargest.c

        #include<stdio.h>
        #include<math.h>
        #include<stdlib.h>

        int main(){
            int temp, arr[10];
            for(int i=0; i<10; ++i){
                arr[i] = rand();
                printf("%dth index: %d\n", i, arr[i]);
            }

            for(int i=0; i<10; ++i){
                for(int j=i+1; j<10; ++j){
                    if(arr[i] > arr[j]){
                        temp = arr[i];
                        arr[i] = arr[j];
                        arr[j] = arr[i];
                    }
                }
            }

            printf("Second largest element is %d.\n", arr[8]);
            return 0;
            
        }

4. printarr.c

        #include<stdio.h>

        int main(){
	
	        int num[10];

            for(int i=0; i<10; ++i){
                printf("Enter the element for index %d: \n", i);
                scanf("%d", &num[i]);
            }

            for(int i=0; i<10; ++i){
                printf("value at %dth index: %d\n", i, num[i]);
            }

            return 0;
            
        }

5. pid.c

        #include<stdio.h>
        #include<stdlib.h>
        #include<unistd.h>

        int main(){
            printf("%d", getpid());
            printf("%d", getppid());
            return 0;
        }

## Observation and Conclusion

Hence, we observed and learnt how to use visual editors in UNIX.
