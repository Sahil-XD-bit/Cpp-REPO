# College Managment Program(CMS);\
```cpp
#include<iostream>
using namespace std;

class student{
    private: 
        int roll_no;
        string name;
        int dob;
        string course;
        string gender;

    public:

        void add_student(){
            cout<< "\n\nEnter student Roll No. : ";
            while(!(cin>> roll_no)){
                cout<< "Invalid input of roll number, Try again\n";
                cin.clear();
                cin.ignore(10000,'\n');
            }
            cout<< "Enter student Name : ";
            cin.ignore();
            getline(cin,name);
            if(!name.empty()){
                name[0] = toupper(name[0]);
            }
            for (int i = 1; i < name.length(); i++) {
                if (name[i - 1] == ' ') {
                    name[i] = toupper(name[i]);
                } else {
                    name[i] = tolower(name[i]);
                }
            }
            cout<< "Enter Date of birth of the student : ";
            cin>> dob;
            cin.ignore(); // clear leftover newline from dob input
            while (true) {
                cout << "Enter gender (Male/Female/Other - case sensitive): ";
                getline(cin, gender);

                if (!gender.empty()) {
                    gender[0] = toupper(gender[0]);
                    for (int i = 1; i < gender.length(); i++) {
                        gender[i] = tolower(gender[i]);
                    }
                }

                if (gender == "Male" || gender == "Female" || gender == "Other") {
                    break;  // valid input, exit loop
                } else {
                    cout << "Invalid gender input. Please try again.\n";
                }
            }

        }


        void view_student(){
            cout<< "Student Roll No. is : "<<roll_no<<endl;
            cout<< "Student Name is : "<<name<<endl;
            cout<< "Date of birth of the student is : "<<dob<<endl;
            cout<< "Gender of the student is : "<<gender<<endl;
            cout<< "Course of the student is : "<<course<<endl;
        }


        void enroll_course(){
            int ch;
            cout<< "1. BCA\n2. B-Tech\n3. Bsc\n4. BBA\n5. MCA\n6. M-Tech\n7. MBA\n";
            cout<< "\nEnter the choice of the course you want to enroll in (1 - 7) : ";
            cin>>ch;
            switch(ch){
                case 1 : 
                        course = "BCA";
                        cout<< "Course is : BCA \nCourse Type - Under Graduate \nCourse Duration - 3 years \nTotal Fees - Rs. 3lkhs \nTimings - Full Time "<<endl;
                        break;
                case 2 : 
                        course = "B-Tech";
                        cout<< "Course is : B-Tech \nCourse Type - Under Graduate \nCourse Duration - 4 years \nTotal Fees - Rs. 10lkhs \nTimings - Full Time"<<endl;
                        break;
                case 3 : 
                        course = "Bsc";
                        cout<< "Course is : Bsc \nCourse Type - Under Graduate \nCourse Duration - 3 years \nTotal Fees - Rs. 4lkhs \nTimings - Full Time"<<endl;
                        break;
                case 4 : 
                        course = "BBA";
                        cout<< "Course is : BBA \nCourse Type - Under Graduate \nCourse Duration - 4 years \nTotal Fees - Rs. 7lkhs \nTimings - Full Time\n"<<endl;
                        break;
                case 5 :
                        course = "MCA";
                        cout<< "Course is :  MCA \nCourse Type - Post Graduate \nCourse Duration - 2 years \nTotal Fees - Rs. 8lkhs \nTimings - Full Time "<<endl;
                        break;
                case 6 : 
                        course = "M-Tech";
                        cout<< "Course is : M-Tech \nCourse Type - Post Graduate \nCourse Duration - 2 years \nTotal Fees - Rs. 8lkhs \nTimings - Full Time "<<endl;
                        break;
                case 7 : 
                        course = "MBA";
                        cout<< "Course is : MBA \nCourse Type - Post Graduate \nCourse Duration - 2 years \nTotal Fees - Rs. 8lkhs \nTimings - Full Time "<<endl;
                        break;
                default : 
                        cout<< "Invalid Course choice! Try again"<<endl;
                        return;
            }
            cout << "\nCourse Enrolled Successfully: " << course << endl;
        }
};



int main(){
    cout<< "\n---------->WELCOME TO COLLEGE MANAGEMENT SYSTEM(CMS) :<----------\n"<<endl;
    int count=0;
    int size;
    cout<< "How many students you want to enter : ";
    cin>>size;
    if(size<=0){
        cout<< "Invalid size, Exiting program!";
        return 0;   
    }
    student* students = new student[size];
    int ch;

    while(1){
        cout<<"\n***************************************\n";
        cout<< "1). Add student.\n";
        cout<< "2). View student.\n";
        cout<< "3). Course Details and Enrollment.\n";
        cout<< "4). Fees details.\n";
        cout<< "5). Attendance details.\n";
        cout<< "0). Quit.\n";
        cout<<"***************************************\n";
        cout<< "Enter your choice : ";
        cin>>ch;
        switch(ch){
            case 1 :
                if(count>=size){
                    cout<<"You cannot add more students , Limit reached!\n";
                    break;
                }
                cout<< "Choice is : Adding Student";
                students[count].add_student();
                cout<< "\nStudent added successfully!"<<endl;
                count++;  
                break;
                
            case 2 :
                if(count==0){
                    cout<<"No student is added! Try after adding students";
                    break;
                }else{
                    cout<< "Choice is : Viewing students\n";
                    for(int i=0 ; i<count ; i++){
                        cout<< "\nStudent "<<i+1<<"\n";
                        students[i].view_student();
                    } 
                    break;
                }

            case 3 : 
                    if(count==0){
                        cout<< "No student is added! Try after adding students";
                    }else{
                        int id;
                        cout<< "Select a student number from(1 to "<<count<<") to enroll: ";
                        cin>>id;
                        if(id <=0 || id > count){
                            cout<< "Invalid student number, Try again!\n";
                        }else{ 
                            students[id-1].enroll_course();
                        }
                    }
                    break;
            case 0 :
                cout<<"\nExiting !"<<endl;
                delete[] students;
                return 0;
            default : cout<< "\nInvalid choice, Try again.\n";
        }
    }
}


```cpp