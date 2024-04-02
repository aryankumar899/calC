#include<iostream>
#include<string>
using namespace std;

class applicant {
public:
    string name, add;
    int age, month_s, total_home_loan, total_personal_loan, n_o_c, com_tier;
    char own_house, spouse_working, depended_parents;

    applicant() {} // Default constructor

    applicant(string name, int age, string add, int month_s, int total_home_loan, int total_personal_loan, int n_o_c, char own_house, char spouse_working, char depended_parents, int com_tier) :
        name(name), age(age), add(add), month_s(month_s), total_home_loan(total_home_loan),
        total_personal_loan(total_personal_loan), n_o_c(n_o_c), own_house(own_house), spouse_working(spouse_working),
        depended_parents(depended_parents), com_tier(com_tier) {}

    int calc_liability() {
        int credit_s = 0;

        // Your liability calculation logic here
        int liability;
            if(age>=22 && age<=30){
                credit_s=credit_s+2;
            }
            else if(age>=30 && age<=35){
                credit_s+=1;
            } 
            else{
                credit_s--;
            }

            liability=total_home_loan+total_personal_loan;
            if(liability==month_s/4){
                credit_s+=5;
            }
            else if(liability>=month_s/4 && liability<=month_s/3){
                credit_s+=3;
            }
            else if(liability>=month_s/3 && liability<=month_s/2){
                credit_s+=1;
            }
            else{
                credit_s--;
            }

            if(n_o_c<=2){
                credit_s-=2;
            }
            else if(n_o_c<=1){
                credit_s-=1;
            }
            else{
                credit_s++;
            }

            if(total_home_loan>=total_personal_loan){
                credit_s++;
            }
            else{
                credit_s--;
            }
            if(own_house=='y' || own_house=='Y'){
                credit_s++;
            }
            else{
                credit_s--;
            }
            if(spouse_working=='y' || spouse_working=='Y'){
                credit_s++;
            }
            else{
                credit_s--;
            }
            if(depended_parents=='y' || depended_parents=='Y'){
                credit_s++;
            }
            if(com_tier==1){
                credit_s+=3;
            }
            else if(com_tier==2){
                credit_s+=2;
            }
            else{
                credit_s++;
            }

        return credit_s;
    }

    void display_score(int score) {
        system("cls");
        if (score > 9) {
            cout << "The applicant " << name << " is at low risk." << endl;
            cout << "Credit score = " << score << endl;
            cout << "Credit can be given." << endl;
        }
        else if (score >= 5 && score < 9) {
            cout << "The applicant " << name << " is at average risk." << endl;
            cout << "Credit score = " << score << endl;
            cout << "Credit can be given with due precautions." << endl;
        }
        else {
            cout << "The applicant " << name << " is at high risk." << endl;
            cout << "Credit score = " << score << endl;
            cout << "Credit cannot be given." << endl;
        }
    }
};

int main() {
    system("cls");
    string name, add;
    int age, month_s, total_home_loan, total_personal_loan, n_o_c, com_tier;
    char own_house, spouse_working, depended_parents;

    cout << "CREDIT CALC" << endl;
    cout << "___________" << endl;

    int opt;
        cout << endl << endl;
        cout << "1- Enter loan applicant's details" << endl;
        cout << "2- Display credit score" << endl;
        cout << "3- Exit" << endl;
        cout << "Select an option by typing the numeric code: ";
        cin >> opt;

        switch (opt) {
            case 1:
    cout << "Name of applicant: ";
    cin >> name;
    cout << "Age: ";
    cin >> age;
    // Input validation for age, salary, loan amounts, etc., can be added here
    cout << "Address: ";
    cin >> add;
    cout << "Monthly Salary: ";
    cin >> month_s;
    cout << "Total Home Loan EMI: ";
    cin >> total_home_loan;
    cout << "Total Personal Loan EMI: ";
    cin >> total_personal_loan;
    cout << "Number of cheque bounces in last six months: ";
    cin >> n_o_c;
    cout << "Own House (y or n): ";
    cin >> own_house;
    cout << "Dependent Parents (y or n): ";
    cin >> depended_parents;
    cout << "Company Tier: ";
    cin >> com_tier;

    // Create an applicant object with entered data
    applicant a(name, age, add, month_s, total_home_loan, total_personal_loan, n_o_c, own_house, spouse_working, depended_parents, com_tier);
    int score = a.calc_liability(); // Calculate liability
    a.display_score(score); // Display credit score
    break;

    } 

    return 0;
}

