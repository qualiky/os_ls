# Labsheet 4: Using the environment variables and argument passing in command line

___

## Objectives

1. To understand the basics of environment variable in UNIX systems.
2. To pass arguments to programs

## Theory  
  
The shell uses environment variables to store information, such as the name of the current user, the name of the host computer, and the default paths to any commands. Environment variables are inherited by all commands executed in the shell’s context, and some commands depend on environment variables.

We can create environment variables and use them to control the behaviour of a command without modifying the command itself. For example, we can use an environment variable to have a command print debug information to the console.

To set the value of an environment variable, we can use the appropriate shell command to associate a variable name with a value. For example, to set the variable PATH to the value `/bin:/sbin:/user/bin:/user/sbin:/system/Library/`, we would enter the following command in a Terminal window:

`% PATH=/bin:/sbin:/user/bin:/user/sbin:/system/Library/ export PATH`

To view all environment variables, we enter:

`% env`

When we launch an app from a shell, the app inherits much of the shell’s environment, including exported environment variables. This form of inheritance can be a useful way to configure the app dynamically. For example, the app can check for the presence (or value) of an environment variable and change its behaviour accordingly.

Although child processes of a shell inherit the environment of that shell, shells are separate execution contexts that don’t share environment information with each other. Variables we set in one Terminal window aren’t set in other Terminal windows.

After we close a Terminal window, variables we set in that window are no longer available. If we want the value of a variable to persist across sessions and in all Terminal windows, we must set it in a shell startup script.

## Activity

1. makefile.c

        #include<stdio.h>
        #include<stdlib.h>

        int main(int argc, char** argv){
            FILE *fs;
            int i;
            if(argc < 2) {
                printf("Too few parameters\n");
                return -2;
            }

            if(argc > 2) {
                printf("Too many arguments!\n");
                return -1;
            }

            fs = fopen(*(*argv+1), "w");
            fclose(fs);

            printf("%d New files created!\n", argc-1);
            return 0;  
        }
2. makemultiplefile.c

        #include<stdio.h>
        #include<stdlib.h>

        int main(int argc, char** argv){
            FILE *fs;
            int i;
            
            for(int k=1; k<argc; ++k){
                fs = fopen(*(argv+k), "w");
                fclose(fs);
            }

            printf("%d New files created!\n", argc-1);
            return 0;  
        }
3. copyfiles.c

        #include<stdio.h>

        int main(int argc, char** argv){
            char ch;
            FILE *fs, *fd;
            if(argc > 3 || argc < 3) {
                printf("Parameter error");
                return -1;
            }

            fs = fopen(*(argv+1), "r");
            fd = fopen(*(argv+2), "w");

            if(fs == NULL){
                printf("Empty source.\n");
                return -1;
            }

            while((ch = getc(fs))!=EOF){
                putc(ch, fd);
            }

            fclose(fs);
            fclose(fd);

            printf("Copied.");

            return 0;

            
        }
4. copymultiple.c

        #include<stdio.h>

        int main(int argc, char** argv){
            char ch;
            FILE *fs, *fd;
            if(argc > 3 || argc < 3) {
                printf("Parameter error");
                return -1;
            }

            fs = fopen(*(argv+1), "r");
            fd = fopen(*(argv+2), "w");

            if(fs == NULL){
                printf("Empty source.\n");
                return -1;
            }

            while((ch = getc(fs))!=EOF){
                putc(ch, fd);
            }

            fclose(fs);
            fclose(fd);

            printf("Copied.");

            return 0;            
        }
5. showenv.c

        #include<stdio.h>
        #include<stdlib.h>

        extern char** environ;

        int main(){
            char** env = environ;

            while(*env){
                printf("%s\n", *env);
                ++env;
            }
            return 0;
        }

## Observation and Conclusion

Hence, we observed and learnt how to use environmental variables and pass parameters to programs.
