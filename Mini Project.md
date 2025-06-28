# College Managment Program(CMP);
```cpp
#include<iostream>
#include<iomanip>
using namespace std;

class student {
private:
    int roll_no;
    string name, dob, course, gender;
    float marks[5];
    float cgpa;
    int total_classes, attended_classes;

public:
    student() {
        for (int i = 0; i < 5; i++) marks[i] = -1;
        cgpa = -1;
        total_classes = attended_classes = 0;
    }

    void add_student() {
        cout << "\nEnter Roll No: ";
        while (!(cin >> roll_no)) {
            cout << "Invalid input! Try again: ";
            cin.clear();
            cin.ignore(10000, '\n');
        }
        cin.ignore();
        cout << "Enter Name: ";
        getline(cin, name);
        cout << "Enter DOB (DD/MM/YYYY): ";
        getline(cin, dob);

        while (true) {
            cout << "Enter Gender (Male/Female/Other): ";
            getline(cin, gender);
            if (gender == "Male" || gender == "Female" || gender == "Other") break;
            else cout << "Invalid gender. Try again.\n";
        }
    }

    void view_student() {
        cout << "\n========== STUDENT INFO ==========";
        cout << "\nName     : " << name;
        cout << "\nRoll No. : " << roll_no;
        cout << "\nDOB      : " << dob;
        cout << "\nGender   : " << gender;
        cout << "\nCourse   : " << (course.empty() ? "Not Enrolled" : course);
        cout << "\nCGPA     : " << (cgpa == -1 ? "Not Entered" : to_string(cgpa).substr(0, 4));
        cout << "\nTotal Classes     : " << total_classes;
        cout << "\nClasses Attended  : " << attended_classes;
        cout << "\n==================================\n";
    }

    void enroll_course() {
        int ch;
        cout << "\nChoose Course:\n";
        cout << "1. BCA\n2. BTech\n3. BSc\n4. BBA\n5. MCA\n6. MTech\n7. MBA\nChoice: ";
        cin >> ch;

        switch (ch) {
            case 1:
                course = "BCA";
                cout << "\nCourse Enrolled: BCA\n";
                cout << "Course Type    : Under Graduate\n";
                cout << "Duration       : 3 years\n";
                cout << "Fees           : Rs. 3 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            case 2:
                course = "BTech";
                cout << "\nCourse Enrolled: BTech\n";
                cout << "Course Type    : Under Graduate\n";
                cout << "Duration       : 4 years\n";
                cout << "Fees           : Rs. 10 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            case 3:
                course = "BSc";
                cout << "\nCourse Enrolled: BSc\n";
                cout << "Course Type    : Under Graduate\n";
                cout << "Duration       : 3 years\n";
                cout << "Fees           : Rs. 4 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            case 4:
                course = "BBA";
                cout << "\nCourse Enrolled: BBA\n";
                cout << "Course Type    : Under Graduate\n";
                cout << "Duration       : 3 years\n";
                cout << "Fees           : Rs. 5 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            case 5:
                course = "MCA";
                cout << "\nCourse Enrolled: MCA\n";
                cout << "Course Type    : Post Graduate\n";
                cout << "Duration       : 2 years\n";
                cout << "Fees           : Rs. 6 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            case 6:
                course = "MTech";
                cout << "\nCourse Enrolled: MTech\n";
                cout << "Course Type    : Post Graduate\n";
                cout << "Duration       : 2 years\n";
                cout << "Fees           : Rs. 7 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            case 7:
                course = "MBA";
                cout << "\nCourse Enrolled: MBA\n";
                cout << "Course Type    : Post Graduate\n";
                cout << "Duration       : 2 years\n";
                cout << "Fees           : Rs. 8 Lakhs\n";
                cout << "Timing         : Full Time\n";
                break;
            default:
                cout << "Invalid choice!\n";
                return;
        }
    }


    void enter_marks() {
        string subjects[5] = { "C++", "DBMS", "Java", "Web", "Maths" };
        float total = 0;
        for (int i = 0; i < 5; i++) {
            float m;
            while (true) {
                cout << "Enter marks for " << subjects[i] << " (0-100): ";
                cin >> m;
                if (m >= 0 && m <= 100) break;
                else cout << "Invalid. Try again.\n";
            }
            marks[i] = m;
            total += m;
        }
        cgpa = (total / 5.0f) / 9.5f;
        cout << "CGPA calculated successfully.\n";
    }

    void enter_attendance() {
        cout << "Enter total classes held: ";
        cin >> total_classes;
        cout << "Enter classes attended: ";
        cin >> attended_classes;
    }
};

int main() {
    int size;
    cout << "Enter number of students: ";
    cin >> size;

    if (size <= 0) {
        cout << "Invalid size. Exiting...\n";
        return 0;
    }

    student* students = new student[size];
    int count = 0;
    int choice;

    while (true) {
        cout << "\n============== MENU ==============\n";
        cout << "1. Add Student\n";
        cout << "2. View All Students\n";
        cout << "3. Enroll in Course\n";
        cout << "4. Enter Marks & CGPA\n";
        cout << "5. Enter Attendance\n";
        cout << "0. Exit\n";
        cout << "==================================\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            if (count >= size) {
                cout << "Student limit reached.\n";
            } else {
                students[count].add_student();
                count++;
                cout << "Student added!\n";
            }
            break;

        case 2:
            if (count == 0) cout << "No students to show.\n";
            else for (int i = 0; i < count; i++) students[i].view_student();
            break;

        case 3: case 4: case 5:
            if (count == 0) {
                cout << "No students available.\n";
            } else {
                int id;
                cout << "Enter student number (1 to " << count << "): ";
                cin >> id;
                if (id <= 0 || id > count) cout << "Invalid ID.\n";
                else {
                    if (choice == 3) students[id - 1].enroll_course();
                    else if (choice == 4) students[id - 1].enter_marks();
                    else students[id - 1].enter_attendance();
                }
            }
            break;

        case 0:
            delete[] students;
            cout << "Exiting program. Goodbye!\n";
            return 0;

        default:
            cout << "Invalid choice. Try again.\n";
        }
    }
}
```cpp
