```cpp
//////////////// Banking System ////////////////

#include<iostream>
using namespace std;

void current_balance(double cb){
    cout << "Your current balance is : $ " << cb << '\n';
}

double deposit(){
    double dep;
    cout << "Enter amount for deposit : $ ";
    cin >> dep;
    return dep;
}

double withdraw(double cb){ 
    double csh;
    cout << "Enter amount to be withdrawn : $ ";
    cin >> csh;
    
    if (csh > cb) {
        cout << "Insufficient balance! Withdrawal failed.\n";
        return cb;  // return original balance, no withdrawal
    }
    
    cb = cb - csh;
    cout << "Amount Withdrawn : $ " << csh << '\n';
    return cb;
}

void new_balance(double cb){
    cout << "Updated amount in your account : $ " << cb << '\n';
}

int main(){
    double cb = 50000;  // initial balance
    double dep;         // deposit amount
    char ch;

    do {
        cout << "Enter your choice for Banking (A - Current Balance, B - Deposit, C - Withdraw, D - New Balance, E - Exit) : ";
        cin >> ch;
        cout << "# # # # # # # # # WELCOME TO BANK # # # # # # # # # \n\n";

        switch(ch){
            case 'A':
            case 'a':{
                current_balance(cb);
                cout << '\n';
                break;
            }
            case 'B':
            case 'b':{
                dep = deposit();
                cb = cb + dep;
                cout << '\n';
                break;
            }
            case 'C':
            case 'c':{
                cb = withdraw(cb);
                cout << '\n';
                break;
            }
            case 'D':
            case 'd':{
                new_balance(cb);
                cout << '\n';
                break;
            }
            case 'E':
            case 'e':{
                cout << "-------  EXIT  -------\n\n";
                break;
            }
            default:{
                cout << "Enter a valid choice!\n\n";
            }
        }
        cout << "# # # # # # # # #    THANK YOU    # # # # # # # # # \n\n";

    } while(ch != 'E' && ch != 'e');

    return 0;
}


// 
// 
// 
// 
// 



//////////////// ROCK PAPER SCISSOR GAME ///////////////

#include<iostream>
#include<ctime>
using namespace std;

int userchoice(){
    int ch1;
    while (true) {
        cout << "\n1. Rock\n2. Paper\n3. Scissor\n4. Exit\n";
        cout << "Enter choice (1-4): ";
        cin >> ch1;

        if (cin.fail()) {
            cin.clear();               // Clear error state
            cin.ignore(1000, '\n');    // Discard bad input
            cout << "Invalid input! Please enter a number (1-4).\n";
            continue;
        }

        if (ch1 >= 1 && ch1 <= 4) {
            switch(ch1){
                case 1:
                    cout << "You chose Rock.\n"; break;
                case 2:
                    cout << "You chose Paper.\n"; break;
                case 3:
                    cout << "You chose Scissor.\n"; break;
                case 4:
                    cout << "Exiting the game.\n"; break;
            }
            return ch1;
        } else {
            cout << "Please enter a valid number between 1 and 4.\n";
        }
    }
}

int compchoice(){
    return (rand() % 3) + 1;
}

void showchoice(int ch1 , int ch2){
    if(ch1 != 4){
        cout << "Computer's choice is : ";
        switch(ch2){
            case 1: cout << "Rock\n"; break;
            case 2: cout << "Paper\n"; break;
            case 3: cout << "Scissor\n"; break;
        }
    } else {
        cout << "User left, so no result.\n";
    }
}

void winner(int ch1 , int ch2){
    if(ch1 >= 1 && ch1 <= 3){
        if(ch1 == ch2){
            cout << "Game resulted in a Draw!\n";
        } else if((ch1 == 1 && ch2 == 2) || (ch1 == 2 && ch2 == 3) || (ch1 == 3 && ch2 == 1)){
            cout << "Computer Won!\n";
        } else {
            cout << "You Won!\n";
        }
    }
}

int main(){
    int ch1, ch2;
    srand(time(NULL)); // Seed only once

    do{
        ch1 = userchoice();
        if(ch1 >= 1 && ch1 <= 3){
            ch2 = compchoice();
            showchoice(ch1, ch2);
            winner(ch1, ch2);
        }
    } while(ch1 != 4);

    cout << "\nThanks for playing!\n";
    return 0;
}



// 
// 
// 
// 




///////////// QUIZ GAMEE /////////////////

#include<iostream>
using namespace std;

//  This function returns 1 if correct, else 0
int check_and_score(char correctans, char userch){
    if(userch == correctans){
        cout << "Correct.\n";
        return 1;
    } else {
        cout << "Incorrect.\n";
        return 0;
    }
}

int main(){
    char ch;
    char userch;
    int score = 0;  //  Total score tracked in main()

    string ques[] = {
        "1). Which car has a bull logo ?",
        "2). Which car has a horse logo ?",
        "3). Which car has a pony logo ?",
        "4). Which car has a devil logo ?"
    };

    string opts[][3] = {
        {"A. Lambo", "B. BMW", "C. Porsche"},
        {"A. Mustang", "B. Ferrari", "C. Corvette"},
        {"A. Chevrolet", "B. Maseratti", "C. Mustang"},
        {"A. Dodge", "B. Mini-Cooper", "C. None"}
    };

    char anskey[] = {'A','B','C','A'};
    int size_q = sizeof(ques)/sizeof(ques[0]);

    cout << "Enter your choice.\n";
    cout << "Press 'S' to start the game.\n";
    cout << "Press 'Q' to quit the game.\n";
    cin >> ch;
    ch = toupper(ch);

    if(ch == 'S'){
        for(int i = 0; i < size_q; i++){
            cout << "\n" << ques[i] << '\n';
            for(int j = 0; j < 3; j++){
                cout << opts[i][j] << "    ";
            }
            cout << '\n';
            cin >> userch;
            userch = toupper(userch);

            //  Add the result (0 or 1) to score
            score += check_and_score(anskey[i], userch);
        }

        //  Print final score
        cout << "\nYour final score is: " << score << " / " << size_q << '\n';
    } else if(ch == 'Q'){
        cout << "You Quit.\n";
    }

    return 0;
}
