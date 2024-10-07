#include <iostream>
using namespace std;

int main() {
    float num1, num2;
    char operasi;

    cout << "Masukkan angka pertama: ";
    cin >> num1;
    cout << "Masukkan operator (+, -, *, /): ";
    cin >> operasi;
    cout << "Masukkan angka kedua: ";
    cin >> num2;

    switch (operasi) {
        case '+':
            cout << "Hasil: " << num1 + num2 << endl;
            break;
        case '-':
            cout << "Hasil: " << num1 - num2 << endl;
            break;
        case '*':
            cout << "Hasil: " << num1 * num2 << endl;
            break;
        case '/':
            if (num2 != 0)
                cout << "Hasil: " << num1 / num2 << endl;
            else
                cout << "Error: Pembagian dengan nol!" << endl;
            break;
        default:
            cout << "Operator tidak valid!" << endl;
            break;
    }

    return 0;
}


