# 1. Write a program to compute the sum of the first n terms of the series.

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

int main(int argc, char* argv[]) {

    int n;

    if (argc > 1)
        n = atoi(argv[1]);

    else {
        cout << "Enter n: ";
        cin >> n;
    }

    int sum = 0;

    for (int i = 1; i <= n; i++)
        sum += i;

    cout << "Sum = " << sum;

    return 0;
}
```

---

# 2. Write a program to remove duplicates from an array.

```cpp
#include <iostream>
using namespace std;

int main() {

    int n;

    cout << "Enter size of array: ";
    cin >> n;

    int arr[100];

    cout << "Enter elements:\n";

    for (int i = 0; i < n; i++)
        cin >> arr[i];

    cout << "Array after removing duplicates:\n";

    for (int i = 0; i < n; i++) {

        bool duplicate = false;

        for (int j = 0; j < i; j++) {

            if (arr[i] == arr[j]) {
                duplicate = true;
                break;
            }
        }

        if (!duplicate)
            cout << arr[i] << " ";
    }

    return 0;
}
```

---

# 3. Write a program that prints occurrences of each alphabet.

```cpp
#include <iostream>
#include <cctype>
using namespace std;

int main() {

    char text[200];

    cin.ignore();

    cout << "Enter text: ";
    cin.getline(text, 200);

    int freq[26] = {0};

    for (int i = 0; text[i] != '\0'; i++) {

        char ch = tolower(text[i]);

        if (ch >= 'a' && ch <= 'z')
            freq[ch - 'a']++;
    }

    cout << "\nAlphabet Occurrences:\n";

    for (int i = 0; i < 26; i++)
        cout << char(i + 'a') << " : " << freq[i] << endl;

    return 0;
}
```

---

# 4. Write a menu driven program for string manipulation.

```cpp
#include <iostream>
using namespace std;

class StringOperations {

public:

    int length(char str[]) {

        int len = 0;

        while (str[len] != '\0')
            len++;

        return len;
    }

    void showAddress(char str[]) {

        for (int i = 0; str[i] != '\0'; i++)
            cout << str[i] << " -> " << (void*)&str[i] << endl;
    }

    void concatenate(char s1[], char s2[]) {

        int i = length(s1);
        int j = 0;

        while (s2[j] != '\0') {
            s1[i] = s2[j];
            i++;
            j++;
        }

        s1[i] = '\0';

        cout << "Concatenated String: " << s1 << endl;
    }

    void compare(char s1[], char s2[]) {

        int i = 0;

        while (s1[i] == s2[i] && s1[i] != '\0' && s2[i] != '\0')
            i++;

        if (s1[i] == s2[i])
            cout << "Strings are Equal";
        else
            cout << "Strings are Not Equal";
    }

    void uppercase(char str[]) {

        for (int i = 0; str[i] != '\0'; i++) {

            if (str[i] >= 'a' && str[i] <= 'z')
                str[i] = str[i] - 32;
        }

        cout << "Uppercase String: " << str;
    }

    void reverse(char str[]) {

        int len = length(str);

        cout << "Reversed String: ";

        for (int i = len - 1; i >= 0; i--)
            cout << str[i];
    }

    void insert(char mainStr[], char insertStr[], int pos) {

        char result[200];

        int i = 0, j = 0, k = 0;

        while (i < pos)
            result[k++] = mainStr[i++];

        while (insertStr[j] != '\0')
            result[k++] = insertStr[j++];

        while (mainStr[i] != '\0')
            result[k++] = mainStr[i++];

        result[k] = '\0';

        cout << "Final String: " << result;
    }
};

int main() {

    StringOperations obj;

    char s1[100], s2[100];

    cout << "Enter first string: ";
    cin >> s1;

    cout << "Enter second string: ";
    cin >> s2;

    int choice;

    cout << "\n1. Address";
    cout << "\n2. Concatenate";
    cout << "\n3. Compare";
    cout << "\n4. Length";
    cout << "\n5. Uppercase";
    cout << "\n6. Reverse";
    cout << "\n7. Insert";

    cout << "\nEnter choice: ";
    cin >> choice;

    switch(choice) {

        case 1:
            obj.showAddress(s1);
            break;

        case 2:
            obj.concatenate(s1, s2);
            break;

        case 3:
            obj.compare(s1, s2);
            break;

        case 4:
            cout << "Length = " << obj.length(s1);
            break;

        case 5:
            obj.uppercase(s1);
            break;

        case 6:
            obj.reverse(s1);
            break;

        case 7:
            int pos;
            cout << "Enter position: ";
            cin >> pos;
            obj.insert(s1, s2, pos);
            break;

        default:
            cout << "Invalid Choice";
    }

    return 0;
}
```

---

# 5. Write a program to merge two ordered arrays.

```cpp
#include <iostream>
using namespace std;

int main() {

    int n1, n2;

    cout << "Enter size of first array: ";
    cin >> n1;

    int a[100];

    cout << "Enter sorted elements:\n";

    for (int i = 0; i < n1; i++)
        cin >> a[i];

    cout << "Enter size of second array: ";
    cin >> n2;

    int b[100];

    cout << "Enter sorted elements:\n";

    for (int i = 0; i < n2; i++)
        cin >> b[i];

    int c[200];

    int i = 0, j = 0, k = 0;

    while (i < n1 && j < n2) {

        if (a[i] < b[j])
            c[k++] = a[i++];

        else
            c[k++] = b[j++];
    }

    while (i < n1)
        c[k++] = a[i++];

    while (j < n2)
        c[k++] = b[j++];

    cout << "Merged Array:\n";

    for (int i = 0; i < n1 + n2; i++)
        cout << c[i] << " ";

    return 0;
}
```

---

# 6(a). Binary Search with recursion

```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int low, int high, int key) {

    if (low > high)
        return -1;

    int mid = (low + high) / 2;

    if (arr[mid] == key)
        return mid;

    else if (key < arr[mid])
        return binarySearch(arr, low, mid - 1, key);

    else
        return binarySearch(arr, mid + 1, high, key);
}

int main() {

    int n;

    cout << "Enter size: ";
    cin >> n;

    int arr[100];

    cout << "Enter sorted elements:\n";

    for (int i = 0; i < n; i++)
        cin >> arr[i];

    int key;

    cout << "Enter element to search: ";
    cin >> key;

    int result = binarySearch(arr, 0, n - 1, key);

    if (result != -1)
        cout << "Element found at index " << result;

    else
        cout << "Element not found";

    return 0;
}
```

---

# 6(b). Binary Search without recursion

```cpp
#include <iostream>
using namespace std;

int main() {

    int n;

    cout << "Enter size: ";
    cin >> n;

    int arr[100];

    cout << "Enter sorted elements:\n";

    for (int i = 0; i < n; i++)
        cin >> arr[i];

    int key;

    cout << "Enter element to search: ";
    cin >> key;

    int low = 0, high = n - 1;

    int found = -1;

    while (low <= high) {

        int mid = (low + high) / 2;

        if (arr[mid] == key) {
            found = mid;
            break;
        }

        else if (key < arr[mid])
            high = mid - 1;

        else
            low = mid + 1;
    }

    if (found != -1)
        cout << "Element found at index " << found;

    else
        cout << "Element not found";

    return 0;
}
```

---

# 7(a). GCD using recursion

```cpp
#include <iostream>
using namespace std;

int gcd(int a, int b) {

    if (b == 0)
        return a;

    return gcd(b, a % b);
}

int main() {

    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    cout << "GCD = " << gcd(a, b);

    return 0;
}
```

---

# 7(b). GCD without recursion

```cpp
#include <iostream>
using namespace std;

int main() {

    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    while (b != 0) {

        int temp = b;
        b = a % b;
        a = temp;
    }

    cout << "GCD = " << a;

    return 0;
}
```

# 8. Create a Matrix class to perform Sum, Product and Transpose.

```cpp
#include <iostream>
using namespace std;

class Matrix {

    int row, col;
    int a[10][10];

public:

    void input() {

        cout << "Enter rows and columns: ";
        cin >> row >> col;

        cout << "Enter elements:\n";

        for (int i = 0; i < row; i++) {

            for (int j = 0; j < col; j++)
                cin >> a[i][j];
        }
    }

    void display() {

        for (int i = 0; i < row; i++) {

            for (int j = 0; j < col; j++)
                cout << a[i][j] << " ";

            cout << endl;
        }
    }

    Matrix add(Matrix m) {

        Matrix result;

        if (row != m.row || col != m.col)
            throw "Addition not possible";

        result.row = row;
        result.col = col;

        for (int i = 0; i < row; i++) {

            for (int j = 0; j < col; j++)
                result.a[i][j] = a[i][j] + m.a[i][j];
        }

        return result;
    }

    Matrix multiply(Matrix m) {

        Matrix result;

        if (col != m.row)
            throw "Multiplication not possible";

        result.row = row;
        result.col = m.col;

        for (int i = 0; i < result.row; i++) {

            for (int j = 0; j < result.col; j++) {

                result.a[i][j] = 0;

                for (int k = 0; k < col; k++)
                    result.a[i][j] += a[i][k] * m.a[k][j];
            }
        }

        return result;
    }

    Matrix transpose() {

        Matrix result;

        result.row = col;
        result.col = row;

        for (int i = 0; i < row; i++) {

            for (int j = 0; j < col; j++)
                result.a[j][i] = a[i][j];
        }

        return result;
    }
};

int main() {

    Matrix m1, m2, result;

    int choice;

    cout << "1. Sum\n2. Product\n3. Transpose\n";
    cout << "Enter choice: ";
    cin >> choice;

    try {

        switch(choice) {

            case 1:
                cout << "Enter first matrix:\n";
                m1.input();

                cout << "Enter second matrix:\n";
                m2.input();

                result = m1.add(m2);

                cout << "Sum Matrix:\n";
                result.display();
                break;

            case 2:
                cout << "Enter first matrix:\n";
                m1.input();

                cout << "Enter second matrix:\n";
                m2.input();

                result = m1.multiply(m2);

                cout << "Product Matrix:\n";
                result.display();
                break;

            case 3:
                cout << "Enter matrix:\n";
                m1.input();

                result = m1.transpose();

                cout << "Transpose Matrix:\n";
                result.display();
                break;

            default:
                cout << "Invalid Choice";
        }
    }

    catch(const char* msg) {
        cout << msg;
    }

    return 0;
}
```

---

# 9. Person, Student and Employee class using runtime polymorphism.

```cpp
#include <iostream>
using namespace std;

class Person {

protected:
    string name;

public:

    void getPerson() {

        cout << "Enter name: ";
        cin >> name;
    }

    virtual void display() {

        cout << "Name: " << name << endl;
    }
};

class Student : public Person {

    string course;
    int marks, year;

public:

    void getStudent() {

        getPerson();

        cout << "Enter course: ";
        cin >> course;

        cout << "Enter marks: ";
        cin >> marks;

        cout << "Enter year: ";
        cin >> year;
    }

    void display() {

        cout << "\nStudent Details\n";

        cout << "Name: " << name << endl;
        cout << "Course: " << course << endl;
        cout << "Marks: " << marks << endl;
        cout << "Year: " << year << endl;
    }
};

class Employee : public Person {

    string department;
    float salary;

public:

    void getEmployee() {

        getPerson();

        cout << "Enter department: ";
        cin >> department;

        cout << "Enter salary: ";
        cin >> salary;
    }

    void display() {

        cout << "\nEmployee Details\n";

        cout << "Name: " << name << endl;
        cout << "Department: " << department << endl;
        cout << "Salary: " << salary << endl;
    }
};

int main() {

    Person* p;

    Student s;
    Employee e;

    int choice;

    cout << "1. Student\n2. Employee\n";
    cout << "Enter choice: ";
    cin >> choice;

    if (choice == 1) {

        s.getStudent();

        p = &s;
        p->display();
    }

    else if (choice == 2) {

        e.getEmployee();

        p = &e;
        p->display();
    }

    else
        cout << "Invalid Choice";

    return 0;
}
```

---

# 10. Triangle class with exception handling and overloaded area functions.

```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Triangle {

    float a, b, c;

public:

    void input() {

        cout << "Enter three sides: ";
        cin >> a >> b >> c;

        if (a <= 0 || b <= 0 || c <= 0)
            throw "Sides must be greater than 0";

        if ((a + b <= c) || (a + c <= b) || (b + c <= a))
            throw "Invalid Triangle";
    }

    float area(float base, float height) {

        return 0.5 * base * height;
    }

    float area() {

        float s = (a + b + c) / 2;

        return sqrt(s * (s - a) * (s - b) * (s - c));
    }
};

int main() {

    Triangle t;

    int choice;

    cout << "1. Right Angled Triangle Area\n";
    cout << "2. Any Triangle Area\n";

    cout << "Enter choice: ";
    cin >> choice;

    try {

        if (choice == 1) {

            float base, height;

            cout << "Enter base and height: ";
            cin >> base >> height;

            cout << "Area = " << t.area(base, height);
        }

        else if (choice == 2) {

            t.input();

            cout << "Area = " << t.area();
        }

        else
            cout << "Invalid Choice";
    }

    catch(const char* msg) {

        cout << msg;
    }

    return 0;
}
```

---

# 11. Store and retrieve Student records using file handling.

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Student {

    int rollNo;
    char name[50];
    char className[20];
    int year;
    float marks;

public:

    void input() {

        cout << "Enter Roll No: ";
        cin >> rollNo;

        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter Class: ";
        cin >> className;

        cout << "Enter Year: ";
        cin >> year;

        cout << "Enter Total Marks: ";
        cin >> marks;
    }

    void display() {

        cout << "\nRoll No: " << rollNo;
        cout << "\nName: " << name;
        cout << "\nClass: " << className;
        cout << "\nYear: " << year;
        cout << "\nMarks: " << marks << endl;
    }
};

int main() {

    Student s;

    ofstream fout("student.txt");

    cout << "Enter details of 5 students:\n";

    for (int i = 0; i < 5; i++) {

        s.input();

        fout.write((char*)&s, sizeof(s));
    }

    fout.close();

    ifstream fin("student.txt");

    cout << "\nStored Student Records:\n";

    for (int i = 0; i < 5; i++) {

        fin.read((char*)&s, sizeof(s));

        s.display();
    }

    fin.close();

    return 0;
}
```

---

# 12. Copy contents of one file to another after removing whitespaces.

```cpp
#include <iostream>
#include <fstream>
#include <cctype>
using namespace std;

int main() {

    ifstream fin("input.txt");

    ofstream fout("output.txt");

    char ch;

    while (fin.get(ch)) {

        if (!isspace(ch))
            fout << ch;
    }

    cout << "File copied successfully without whitespaces.";

    fin.close();
    fout.close();

    return 0;
}
```
