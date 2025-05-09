# FOCP-Assignment-SEM-2
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Student class definition
class Student {
private:
    string name;
    int rollNumber;
    float cgpa;
    vector<string> courses;

public:
    // Default constructor
    Student() : name("Unknown"), rollNumber(0000), cgpa(0.0) {}

    // Parameterized constructor
    Student(string n, int r, float c) {
        name = n;
        rollNumber = r;
        if (c >= 0.0 && c <= 10.0)
            cgpa = c;
        else {
            cgpa = 0.0;
            cout << "Invalid CGPA. CGPA is set to 0.0" << endl;
        }
    }

    // Copy constructor
    Student(const Student &other) {
        name = other.name;
        rollNumber = other.rollNumber;
        cgpa = other.cgpa;
        courses = other.courses;
    }

    // Add course
    void addCourse(const string &course) {
        if (!course.empty()) {
            courses.push_back(course);
        } else {
            cout << "Invalid course name." << endl;
        }
    }

    // Update CGPA
    void updateCGPA(float newCGPA) {
        if (newCGPA >= 0.0 && newCGPA <= 10.0) {
            cgpa = newCGPA;
        } else {
            cout << "Invalid CGPA. Please enter a value between 0.0 and 10.0" << endl;
        }
    }

    // Display student information
    void displayInfo() const {
        cout << "Name: " << name
             << "\nRoll Number: " << rollNumber
             << "\nCGPA: " << cgpa
             << "\nCourses: ";
        if (courses.empty()) {
            cout << "None";
        } else {
            for (size_t i = 0; i < courses.size(); ++i) {
                cout << courses[i];
                if (i != courses.size() - 1)
                    cout << ", ";
            }
        }
        cout << "\n------------------------" << endl;
    }

    // Getter for roll number
    int getRollNumber() const {
        return rollNumber;
    }
};

// Management system for handling students
class StudentManagementSystem {
private:
    vector<Student> students;

public:
    // Add a new student
    void addStudent(const Student &student) {
        students.push_back(student);
    }

    // Search student by roll number
    Student* searchStudent(int rollNumber) {
        for (auto &student : students) {
            if (student.getRollNumber() == rollNumber)
                return &student;
        }
        return nullptr;
    }

    // Display all students
    void displayAllStudents() const {
        if (students.empty()) {
            cout << "No student records available." << endl;
            return;
        }
        for (const auto &student : students) {
            student.displayInfo();
        }
    }
};

// Main function
int main() {
    StudentManagementSystem sms;

    // Creating students
    Student s1("alice", 101, 9.5);
    Student s2("bob", 102, 8.7);
    Student s3 = s1; // Copy constructor

    // Adding courses
    s1.addCourse("Mathematics");
    s1.addCourse("Physics");
    s2.addCourse("Chemistry");

    // Updating CGPA
    s1.updateCGPA(9.8);

    // Adding students to management system
    sms.addStudent(s1);
    sms.addStudent(s2);
    sms.addStudent(s3);

    // Display all student information
    sms.displayAllStudents();

    // Search student
    int roll;
    cout << "Enter roll number to search: ";
    cin >> roll;
    Student* result = sms.searchStudent(roll);
    if (result)
        result->displayInfo();
    else
        cout << "Student not found." << endl;

    return 0;
