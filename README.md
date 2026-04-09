# EncryptionTool
#include <string>
#include <iostream>
#include <fstream>
using namespace std;

string encryptText(string message, int key) {
    string encrypted = "";
    
    for (int i = 0; i < message.length(); i++) {
       
        char encryptedChar = message[i] ^ key;
        encrypted += encryptedChar;
    }
    
    return encrypted;
}


string decryptText(string message, int key) {
    string decrypted = "";
    
    for (int i = 0; i < message.length(); i++) {
        
        char decryptedChar = message[i] ^ key;
        decrypted += decryptedChar;
    }
    
    return decrypted;
}

// Save encrypted message to file
void saveToFile(string filename, string content) {
    ofstream file(filename);
    
    if (file.is_open()) {
        file << content;
        file.close();
        cout << "File saved: " << filename << endl;
    } else {
        cout << "Error: Cannot create file!" << endl;
    }
}

string readFromFile(string filename) {
    ifstream file(filename);
    string content = "";
    
    if (file.is_open()) {
        char ch;
        while (file.get(ch)) {
            content += ch;
        }
        file.close();
    } else {
        cout << "Error: Cannot open file!" << endl;
    }
    
    return content;
}


void showMenu() {
    cout << "\n==== TEXT ENCRYPTION TOOL ====" << endl;
    cout << "1. Encrypt text" << endl;
    cout << "2. Decrypt text" << endl;
    cout << "3. Encrypt text from file" << endl;
    cout << "4. Decrypt text from file" << endl;
    cout << "5. Exit" << endl;
    cout << "==============================" << endl;
}

int main() {
    int choice;
    string message;
    int encryptionKey;
    string filename;
    
    cout << "Welcome to Simple Encryption Tool!" << endl;
    cout << "Encryption Key is a number between 1-255" << endl;
    
    while (true) {
        showMenu();
        cout << "Enter your choice (1-5): ";
        cin >> choice;
        cin.ignore(); 
        
        if (choice == 1) {
            
            cout << "\nEnter text to encrypt: ";
            getline(cin, message);
            
            cout << "Enter encryption key (1-255): ";
            cin >> encryptionKey;
            cin.ignore();
            
            string encrypted = encryptText(message, encryptionKey);
            
            cout << "\nOriginal text: " << message << endl;
            cout << "Encrypted text: " << encrypted << endl;
            
            cout << "\nDo you want to save to file? (y/n): ";
            char response;
            cin >> response;
            
            if (response == 'y' || response == 'Y') {
                cout << "Enter filename: ";
                cin.ignore();
                getline(cin, filename);
                saveToFile(filename, encrypted);
            }
        }
        else if (choice == 2) {
           
            cout << "\nEnter text to decrypt: ";
            getline(cin, message);
            
            cout << "Enter decryption key (1-255): ";
            cin >> encryptionKey;
            cin.ignore();
            
            string decrypted = decryptText(message, encryptionKey);
            
            cout << "\nEncrypted text: " << message << endl;
            cout << "Decrypted text: " << decrypted << endl;
        }
        else if (choice == 3) {
            
            cout << "\nEnter input filename: ";
            getline(cin, filename);
            
            message = readFromFile(filename);
            
            if (message != "") {
                cout << "Enter encryption key (1-255): ";
                cin >> encryptionKey;
                cin.ignore();
                
                string encrypted = encryptText(message, encryptionKey);
                
                cout << "\nOriginal text from file: " << message << endl;
                cout << "Encrypted text: " << encrypted << endl;
                
                cout << "\nEnter output filename: ";
                getline(cin, filename);
                saveToFile(filename, encrypted);
            }
        }
        else if (choice == 4) {
           
            cout << "\nEnter input filename: ";
            getline(cin, filename);
            
            message = readFromFile(filename);
            
            if (message != "") {
                cout << "Enter decryption key (1-255): ";
                cin >> encryptionKey;
                cin.ignore();
                
                string decrypted = decryptText(message, encryptionKey);
                
                cout << "\nEncrypted text from file: " << message << endl;
                cout << "Decrypted text: " << decrypted << endl;
            }
        }
        else if (choice == 5) {
            cout << "\nThank you for using Encryption Tool!" << endl;
            break;
        }
        else {
            cout << "\nInvalid choice! Please try again." << endl;
        }
    }
    
    return 0;
}
