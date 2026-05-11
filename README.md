```cpp
// 1. Sum of first n terms of series (1 + 2 + 3 + ... + n)

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

```cpp
// 2. Remove duplicates from array

#include <iostream>
using namespace std;

int main() {
    int n;

    cout << "Enter size of array: ";
    cin >> n;

    int arr[n];

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

```cpp
// 3. Count occurrence of alphabets using command line arguments

#include <iostream>
#include <cstring>
using namespace std;

int main(int argc, char* argv[]) {
    int freq[26] = {0};

    for (int i = 1; i < argc; i++) {
        for (int j = 0; argv[i][j] != '\0'; j++) {

            char ch = tolower(argv[i][j]);

            if (ch >= 'a' && ch <= 'z')
                freq[ch - 'a']++;
        }
    }

    cout << "Alphabet Occurrences:\n";

    for (int i = 0; i < 26; i++)
        cout << char(i + 'a') << " : " << freq[i] << endl;

    return 0;
}
```

---

```cpp
// 4. Menu driven string manipulation program

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

        cout << "Concatenated String: " << s1;
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

        for (int i = len - 1; i >= 0; i--)
            cout << str[i];

    }

    void insert(char mainStr[], char insertStr[], int pos) {

        char result[200];

        int i = 0, j = 0, k = 0;

        while (i < pos) {
            result[k++] = mainStr[i++];
        }

        while (insertStr[j] != '\0') {
            result[k++] = insertStr[j++];
        }

        while (mainStr[i] != '\0') {
            result[k++] = mainStr[i++];
        }

        result[k] = '\0';

        cout << "Final String: " << result;
    }
};

int main() {

    StringOperations obj;

    char s1[100], s2[100];

    int choice;

    cout << "Enter first string: ";
    cin >> s1;

    cout << "Enter second string: ";
    cin >> s2;

    cout << "\n1. Address\n2. Concatenate\n3. Compare\n4. Length\n5. Uppercase\n6. Reverse\n7. Insert\n";
    cout << "Enter choice: ";
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

```cpp
// 5. Merge two ordered arrays

#include <iostream>
using namespace std;

int main() {

    int n1, n2;

    cout << "Enter size of first array: ";
    cin >> n1;

    int a[n1];

    cout << "Enter sorted elements:\n";
    for (int i = 0; i < n1; i++)
        cin >> a[i];

    cout << "Enter size of second array: ";
    cin >> n2;

    int b[n2];

    cout << "Enter sorted elements:\n";
    for (int i = 0; i < n2; i++)
        cin >> b[i];

    int c[n1 + n2];

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

```cpp
// 6a. Binary Search with recursion

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

    int arr[n];

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

```cpp
// 6b. Binary Search without recursion

#include <iostream>
using namespace std;

int main() {

    int n;

    cout << "Enter size: ";
    cin >> n;

    int arr[n];

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

```cpp
// 7a. GCD with recursion

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

```cpp
// 7b. GCD without recursion

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

