# Glory
My first repository<br>
-sahil<br>
```c
//wap to store info about the college students,teachers,staff
#include<stdio.h>
#include<string.h>

typedef struct studentdetails{
    char name[50];
    int rollno;
    float attend;
    float cgpa;
    char course[50];
    float maths,cpp,webdesign,java,dbms;
}Std;

typedef struct teacherdetails{
    char name[50];
    unsigned int id;
    int attend;
    char course[50];
}TD;

typedef struct staffdetails{
    char name[50];
    int tag;
    char job[50];
    int attend;
}SD;

void addstudent();
void viewstudents();
void calculate_attendance(int index);
void calculateCGPA();
void viewCGPA();

int studentcount=0;
Std students[300];

int main(){
    int choice;

    while(1){
        printf("\n====COLLEGE MANAGEMENT SYSTEM====");
        printf("\n1. ADD STUDENT");
        printf("\n2. CALCULATE CGPA");
        printf("\n3. VIEW STUDENT");
        printf("\n4. CALCULATE ATTENDANCE(ONLY)");
        printf("\n5. EXIT");
        printf("\nENTER YOUR CHOICE : ");
        scanf("%d",&choice);

        switch(choice){
        case 1: addstudent();
        break;
        case 2: calculateCGPA();
        break;
        case 3: if( studentcount == 0){
                    printf("No student has been added !\n");
                }else{
                viewstudents();
                }     
        break;
        case 4: calculate_attendance(studentcount);
        break;
        case 5: printf("\nExiting... THANK YOU!");
        return 0;
        default:printf("\nINVALID CHOICE... TRY AGAIN");
        }
    }
    return 0;
}

//function to add student
void addstudent(){
    if (studentcount<300){
        while(1){
            //name
            printf("Enter student name : ");
            getchar();
            fgets(students[studentcount].name,50,stdin);
            students[studentcount].name[strcspn(students[studentcount].name, "\n")] = 0; // Remove newline
            // Check if name is empty after trimming the newline
            if (students[studentcount].name[0] == '\0') {
                printf("Invalid input. Name cannot be empty.\n");
                continue;
            }
            int is_empty=1;   // check if name is not empty
            for (int i = 0 ; students[studentcount].name[i] != '\0' ; i++){
                if(students[studentcount].name[i] != ' '){
                    is_empty = 0;
                    break;
                }
            }
            if (is_empty==1){
                printf("\nInvalid Input . Try again\n");
                continue;
            }
            int valid=1;
            for (int i = 0; students[studentcount].name[i] != '\0'; i++) {  
                 if (!((students[studentcount].name[i] >= 'A' && students[studentcount].name[i] <= 'Z') ||
                    (students[studentcount].name[i] >= 'a' && students[studentcount].name[i] <= 'z') ||
                    (students[studentcount].name[i] == ' '))) {
                    valid=0;
                    break;
                }
            }if (valid) {
                break;
            } else {
                printf("\nInvalid input. TRY AGAIN\n");
            }
        }
        //roll number
        int valid1=0;    
        while(!valid1){
            printf("\nEnter roll number : ");
            if(scanf("%d",&students[studentcount].rollno)==1){
                valid1=1;
            }
            else{
                printf("Invalid input. Enter numeric values.\n");
            }
            while(getchar() !='\n');
        }
        //attendance
        printf("Give details for attendance of student %s : \n",students[studentcount].name);
        calculate_attendance(studentcount);
        printf("\n");
    
        //marks
        const char subjects[][30] = {"MATHS", "C++", "WEBDESIGN", "JAVA", "DBMS"};
        float *marks[] = {&students[studentcount].maths,
                &students[studentcount].cpp, 
                &students[studentcount].webdesign, 
                &students[studentcount].java, 
                &students[studentcount].dbms};

        for (int i = 0; i < 5; i++) {
            while (1) {
                printf("Marks in %s: ", subjects[i]);
                if (scanf("%f", marks[i]) == 1 && *marks[i] >= 0 && *marks[i] <= 100) {
                    break;  // Valid input, exit loop
                } else {
                    printf("Input Invalid. Enter a number between 0 and 100.\n");
                    while (getchar() != '\n'); 
                }    
            }         
        }
        //course
        while(1){
            printf("Course of student : ");
            getchar();
            fgets(students[studentcount].course,50,stdin);
            students[studentcount].course[strcspn(students[studentcount].course, "\n")] = 0; // Remove newline
            if (students[studentcount].course[0] == '\0') {
                printf("Invalid input. Name cannot be empty.\n");
                continue;
            }
            int valid=1;
                for (int i = 0; students[studentcount].course[i] != '\0'; i++) {  
                    if (!((students[studentcount].course[i] >= 'A' && students[studentcount].course[i] <= 'Z') ||
                    (students[studentcount].course[i] >= 'a' && students[studentcount].course[i] <= 'z') ||
                    (students[studentcount].course[i] == ' '))) {
                    valid=0;
                    break;
                }
            }if (valid) {
                break;
            } else {
                printf("\nInvalid input. TRY AGAIN\n");
            }
        }    
        studentcount++;
        printf("\nStudent added successfully");
    }else
    printf("\nStudent list is full!");
}    

void calculate_attendance(int index){
    /*if (studentcount == 0) {
        printf("No students have been added yet!\n");
        return; // Exit the function if no students
    }*/
    int total_classes;
    int attended;
    float total_attendance;
    while(1){
        printf("Enter the total number of classes : ");
        if(scanf("%d",&total_classes) == 1 && total_classes >0){
            break;
        }
        printf("Invalid Input . Please enter a positive number.\n");
        while(getchar() !='\n');  
    }
    while(1){
        printf("Enter the number of days attended : ");
        if(scanf("%d",&attended) == 1 && attended >=0 && attended <=total_classes){
            break;
        }
        printf("Invalid Input. Please enter a number between 0 and %d.\n", total_classes);
        while(getchar() !='\n');  
    }
    total_attendance = ((float)attended/total_classes)*100;
    printf("Total attendance of student is : %.2f%%",total_attendance);
    students[index].attend = total_attendance;
}

void calculateCGPA(){
    int roll;
    
    printf("\nEnter roll numbers to calculate CGPA (Enter -1 to stop):\n");

    while (1) {
        printf("Enter roll number: ");
        if (scanf("%d", &roll) != 1) {
            printf("Invalid input. Please enter a valid roll number.\n");
            while (getchar() != '\n');  // Clear input buffer
            continue;
        }

        if (roll == -1) {
            printf("Exiting CGPA calculation.\n");
            break;
        }

        int found = 0;
        for (int i = 0; i < studentcount; i++) {
            if (students[i].rollno == roll) {
                found = 1;
                float total = students[i].maths + students[i].cpp + students[i].webdesign + students[i].java + students[i].dbms;
                float percentage = (total / 500.00) * 100;
                students[i].cgpa = (total / 500.00) * 10; 

                printf("\nStudent: %s (Roll No: %d)\n", students[i].name, students[i].rollno);
                printf("Total Marks: %.2f / 500\n", total);
                printf("Percentage: %.2f%%\n", percentage);
                printf("CGPA: %.2f\n", students[i].cgpa);
                printf("-------------------------------\n");
                break;
            }
        }

        if (!found) {
            printf("Student with Roll No %d not found. Try again.\n", roll);
        }
    }
}

void viewstudents(){
    printf("\n===== Student Details =====\n");
    
    for(int i=0;i<studentcount;i++){
        printf("\nStudent %d is :\n",i+1);
        printf("Name of student : %s\n",students[i].name);
        printf("Roll number of student : %d\n",students[i].rollno);
        printf("Attendance of student : %.2f%%\n",students[i].attend);
        printf("CGPA of student : %.2f\n",students[i].cgpa);
        printf("Course of student : %s\n",students[i].course);
        printf("Marks : -> MATHS: %.2f\n  -> C++: %.2f\n  -> WEBDESIGN: %.2f\n  -> JAVA: %.2f\n  -> DBMS: %.2f\n" ,
        students[i].maths, students[i].cpp, students[i].webdesign, students[i].java, students[i].dbms);
    }
}

```c