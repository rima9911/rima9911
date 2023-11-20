- 👋 Hi, I’m @rima9911
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
#include <iostream>
#include <ctime>

class Employee {
private:
    std::string name;
    double salary;
    tm hireDate;

public:
    // Constructor
    Employee(const std::string& n, double s, int year, int month, int day) : name(n), salary(s) {
        hireDate = {0, 0, 0, day, month - 1, year - 1900};
    }

    // Friend function to calculate years of service
    friend int calculateYearsOfService(const Employee& emp);
};

// Friend function definition
int calculateYearsOfService(const Employee& emp) {
    std::time_t currentTime = std::time(nullptr);
    tm* now = std::localtime(&currentTime);

    int years = now->tm_year - emp.hireDate.tm_year;

    return (now->tm_mon < emp.hireDate.tm_mon || (now->tm_mon == emp.hireDate.tm_mon && now->tm_mday < emp.hireDate.tm_mday)) ? years - 1 : years;
}

int main() {
    // Create an Employee object
    Employee emp("John Doe", 50000.0, 2010, 5, 15);

    // Calculate and display years of service
    std::cout << "Employee: " << emp.getName() << "\n";
    std::cout << "Salary: $" << emp.getSalary() << "\n";
    std::cout << "Years of Service: " << calculateYearsOfService(emp) << " years\n";

    return 0;
}

