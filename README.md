## Hi there 👋

#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

// Student structure to store student information
struct Student {
    int id;
    string name;
    int age;
    double score;
    
    // Constructor to qqq initialize student data
    Student(int studentId, string studentName, int studentAge, double studentScore) 
        : id(studentId), name(studentName), age(studentAge), score(studentScore) {}
};

// Class to manage student records
class StudentManager {
private:
    vector<Student> students;  // Vector to store all student objects
    
public:
    // Function to add a new student to the system
    void addStudent(int id, string name, int age, double score) {
        Student newStudent(id, name, age, score);
        students.push_back(newStudent);
        cout << "Student added successfully!" << endl;
    }
    
    // Function to display all students in the system
    void displayAllStudents() {
        if (students.empty()) {
            cout << "No students found in the system." << endl;
            return;
        }
        
        cout << "\n--- All Students ---" << endl;
        for (const auto& student : students) {
            cout << "ID: " << student.id << ", Name: " << student.name 
                 << ", Age: " << student.age << ", Score: " << student.score << endl;
        }
    }
    
    // Function to search for a student by ID
    void searchStudentById(int id) {
        auto it = find_if(students.begin(), students.end(), 
                         [id](const Student& s) { return s.id == id; });
        
        if (it != students.end()) {
            cout << "Student found:" << endl;
            cout << "ID: " << it->id << ", Name: " << it->name 
                 << ", Age: " << it->age << ", Score: " << it->score << endl;
        } else {
            cout << "Student with ID " << id << " not found." << endl;
        }
    }
    
    // Function to update student information
    void updateStudent(int id, string name, int age, double score) {
        auto it = find_if(students.begin(), students.end(), 
                         [id](const Student& s) { return s.id == id; });
        
        if (it != students.end()) {
            it->name = name;
            it->age = age;
            it->score = score;
            cout << "Student information updated successfully!" << endl;
        } else {
            cout << "Student with ID " << id << " not found." << endl;
        }
    }
    
    // Function to delete a student from the system
    void deleteStudent(int id) {
        auto it = remove_if(students.begin(), students.end(), 
                           [id](const Student& s) { return s.id == id; });
        
        if (it != students.end()) {
            students.erase(it, students.end());
            cout << "Student deleted successfully!" << endl;
        } else {
            cout << "Student with ID " << id << " not found." << endl;
        }
    }
    
    // Function to calculate average score of all students
    double calculateAverageScore() {
        if (students.empty()) {
            return 0.0;
        }
        
        double totalScore = 0.0;
        for (const auto& student : students) {
            totalScore += student.score;
        }
        
        return totalScore / students.size();
    }
    
    // Function to display students sorted by score in descending order
    void displayStudentsByScore() {
        vector<Student> sortedStudents = students;
        sort(sortedStudents.begin(), sortedStudents.end(), 
             [](const Student& a, const Student& b) { return a.score > b.score; });
        
        cout << "\n--- Students Sorted by Score (Descending) ---" << endl;
        for (const auto& student : sortedStudents) {
            cout << "Name: " << student.name << ", Score: " << student.score << endl;
        }
    }
    
    // Function to get total number of students
    int getTotalStudents() {
        return students.size();
    }
};

int main() {
    StudentManager manager;  // Create student manager object
    
    // Add some sample students
    manager.addStudent(101, "Alice Johnson", 20, 85.5);
    manager.addStudent(102, "Bob Smith", 19, 92.0);
    manager.addStudent(103, "Charlie Brown", 21, 78.5);
    manager.addStudent(104, "Diana Prince", 20, 96.0);
    
    // Display all students
    manager.displayAllStudents();
    
    // Search for a specific student
    cout << "\n--- Searching for student with ID 102 ---" << endl;
    manager.searchStudentById(102);
    
    // Update student information
    cout << "\n--- Updating student with ID 103 ---" << endl;
    manager.updateStudent(103, "Charlie Updated", 22, 82.0);
    
    // Display all students after update
    manager.displayAllStudents();
    
    // Display students sorted by score
    manager.displayStudentsByScore();
    
    // Calculate and display average score
    double average = manager.calculateAverageScore();
    cout << "\n--- Average Score ---" << endl;
    cout << "Average score of all students: " << average << endl;
    
    // Display total number of students
    cout << "\n--- Student Statistics ---" << endl;
    cout << "Total number of students: " << manager.getTotalStudents() << endl;
    
    // Delete a student
    cout << "\n--- Deleting student with ID 101 ---" << endl;
    manager.deleteStudent(101);
    
    // Display final list of students
    manager.displayAllStudents();
    
    return 0;
}
