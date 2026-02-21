# CGPA-Calculator
#include <iostream>
#include <iomanip>
#include <vector>
using namespace std;

class Course {
public:
    string name;
    float grade;
    int credit;
    float gradePoints;

    void inputCourse(int i) {
        cout << "\nEnter details for Course " << i+1 << endl;
        cout << "Course Name     : ";
        cin >> name;
        cout << "Grade (0-10)   : ";
        cin >> grade;
        cout << "Credit Hours   : ";
        cin >> credit;

        gradePoints = grade * credit;
    }

    void displayCourse(int i) {
        cout << "| " << setw(3) << i+1
             << " | " << setw(12) << name
             << " | " << setw(6) << grade
             << " | " << setw(7) << credit
             << " | " << setw(12) << gradePoints
             << " |" << endl;
    }
};

class CGPACalculator {
private:
    vector<Course> courses;
    float totalCredits = 0;
    float totalGradePoints = 0;
    float cgpa = 0;

public:

    void inputData() {
        int n;
        cout << "\nEnter number of courses: ";
        cin >> n;

        courses.resize(n);

        for(int i = 0; i < n; i++) {
            courses[i].inputCourse(i);
            totalCredits += courses[i].credit;
            totalGradePoints += courses[i].gradePoints;
        }

        cgpa = totalGradePoints / totalCredits;
    }

    void displayResult() {

        cout << "\n\n";
        cout << "=============================================================\n";
        cout << "                STUDENT CGPA REPORT SYSTEM                   \n";
        cout << "=============================================================\n";

        cout << "| No  | Course Name  | Grade  | Credits | Grade Points |\n";
        cout << "-------------------------------------------------------------\n";

        for(int i = 0; i < courses.size(); i++) {
            courses[i].displayCourse(i);
        }

        cout << "-------------------------------------------------------------\n";

        cout << "\nTotal Credits      : " << totalCredits << endl;
        cout << "Total GradePoints  : " << totalGradePoints << endl;
        cout << "Final CGPA         : " << fixed << setprecision(2) << cgpa << endl;

        cout << "=============================================================\n";
    }
};

int main() {

    CGPACalculator student;

    cout << "=============================================================\n";
    cout << "          CodeAlpha Internship - CGPA Calculator             \n";
    cout << "=============================================================\n";

    student.inputData();
    student.displayResult();

    return 0;
}
