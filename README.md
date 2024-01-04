# PF Project 3

Sharuf Zaryab Khan  231633.
Course: Programming Fundamentals
Instructor: Dr. Ashfaq Hussain Farooqi
Class: BSCS-IB
Project 3: Clothes Management System.

#include <iostream>
#include <fstream>
#include <string>
using namespace std;

struct Cloth {
    int clothId;
    string clothName;
    int quantity;
    int price;
};

struct Shop {
    int shopId;
    string shopName;
};

struct Registration {
    int shopId;
    string shopType;
};


void addClothes();
void viewClothRecords();
void searchClothRecord();
void updateClothRecord();
void deleteClothRecord();
void addShop();
void viewShopRecords();
void updateShop();
void shopRegistration();
void viewRegistrations();
void exitSystem();

int main() {
    int choice;
    do {
        cout << "\nManagement System\n"
            << "1. Cloth Management\n"
            << "2. Shop Management\n"
            << "3. Shop Registration\n"
            << "4. View Registrations\n"
            << "5. Exit\n"
            << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            int clothChoice;
            do {
                cout << "\nCloth Management\n"
                    << "1. Add Cloth\n"
                    << "2. Search Cloth Record\n"
                    << "3. View Cloth Records\n"
                    << "4. Update Cloth Record\n"
                    << "5. Delete Cloth Record\n"
                    << "6. Back to Main Menu\n"
                    << "Enter your choice: ";
                cin >> clothChoice;

                switch (clothChoice) {
                case 1:
                    addClothes();
                    break;
                case 2:
                    searchClothRecord();
                    break;
                case 3:
                    viewClothRecords();
                    break;
                case 4:
                    updateClothRecord();
                    break;
                case 5:
                    deleteClothRecord();
                    break;
                case 6:
                    break; 
                default:
                    cout << "Incorrect choice\n";
                }
            } while (clothChoice != 6);
            break;

        case 2:
            int shopChoice;
            do {
                cout << "\nShop Management\n"
                    << "1. Add Shop\n"
                    << "2. View Shop Records\n"
                    << "3. Update Shop\n"
                    << "4. Back to Main Menu\n"
                    << "Enter your choice: ";
                cin >> shopChoice;

                switch (shopChoice) {
                case 1:
                    addShop();
                    break;
                case 2:
                    viewShopRecords();
                    break;
                case 3:
                    updateShop();
                    break;
                case 4:
                    break; 
                default:
                    cout << "Incorrect choice\n";
                }
            } while (shopChoice != 4);
            break;

        case 3:
            shopRegistration();
            break;

        case 4:
            viewRegistrations();
            break;

        case 5:
            exitSystem();
            break;

        default:
            cout << "Incorrect choice\n";
        }
    } while (choice != 5);

    return 0;
}

void addClothes() {
    ofstream fout("ClothRecords.txt", ios::app);
    Cloth cloth;

    cout << "Enter Cloth ID: ";
    cin >> cloth.clothId;

    cin.ignore(); 
    cout << "Enter Cloth Name: ";
    cin>>cloth.clothName;

    cout << "Enter Quantity: ";
    cin >> cloth.quantity;
    cout << "Enter Price: ";
    cin >> cloth.price;

    fout << cloth.clothId << " " << cloth.clothName << " " << cloth.quantity << " " << cloth.price << endl;
    fout.close();
}

void viewClothRecords() {
    ifstream fin("ClothRecords.txt");
    Cloth cloth;

    cout << "Cloth Records\n";
    cout << "ID\tName\tQuantity\tPrice\n";
    while (fin >> cloth.clothId >> cloth.clothName >> cloth.quantity >> cloth.price) {
        cout << cloth.clothId << "\t" << cloth.clothName << "\t" << cloth.quantity << "\t\t" << cloth.price << endl;
    }
    fin.close();
}

void searchClothRecord() {
    ifstream fin("ClothRecords.txt");
    Cloth cloth;
    int searchId;

    cout << "Enter Cloth ID to search: ";
    cin >> searchId;

    bool found = false;
    while (fin >> cloth.clothId >> cloth.clothName >> cloth.quantity >> cloth.price) {
        if (cloth.clothId == searchId) {
            found = true;
            cout << "Cloth found with details:\n";
            cout << "ID: " << cloth.clothId << endl;
            cout << "Name: " << cloth.clothName << endl;
            cout << "Quantity: " << cloth.quantity << endl;
            cout << "Price: " << cloth.price << endl;
            break;
        }
    }

    if (!found) {
        cout << "Cloth not found!\n";
    }
    fin.close();
}

void updateClothRecord() {
    ifstream fin("ClothRecords.txt");
    ofstream fout("Temp.txt");
    Cloth cloth;
    int updateId;

    cout << "Enter Cloth ID to update: ";
    cin >> updateId;

    bool found = false;
    while (fin >> cloth.clothId >> cloth.clothName >> cloth.quantity >> cloth.price) {
        if (cloth.clothId == updateId) {
            found = true;
            cout << "Enter updated details:\n";
            cout << "New Name: ";
            cin>>cloth.clothName;
            cout << "New Quantity: ";
            cin >> cloth.quantity;
            cout << "New Price: ";
            cin >> cloth.price;
            fout << cloth.clothId << " " << cloth.clothName << " " << cloth.quantity << " " << cloth.price << endl;
            cout << "Record updated successfully!\n";
        }
        else {
            fout << cloth.clothId << " " << cloth.clothName << " " << cloth.quantity << " " << cloth.price << endl;
        }
    }

    if (!found) {
        cout << "Cloth not found!\n";
    }

    fin.close();
    fout.close();
    remove("ClothRecords.txt");
    rename("Temp.txt", "ClothRecords.txt");
}

void deleteClothRecord() {
    ifstream fin("ClothRecords.txt");
    ofstream fout("Temp.txt");
    Cloth cloth;
    int deleteId;

    cout << "Enter Cloth ID to delete: ";
    cin >> deleteId;

    bool found = false;
    while (fin >> cloth.clothId >> cloth.clothName >> cloth.quantity >> cloth.price) {
        if (cloth.clothId == deleteId) {
            found = true;
            cout << "Record deleted successfully!\n";
        }
        else {
            fout << cloth.clothId << " " << cloth.clothName << " " << cloth.quantity << " " << cloth.price << endl;
        }
    }

    if (!found) {
        cout << "Cloth not found!\n";
    }

    fin.close();
    fout.close();
    remove("ClothRecords.txt");
    rename("Temp.txt", "ClothRecords.txt");
}

void addShop() {
    ofstream fout("ShopRecords.txt", ios::app);
    Shop shop;

    cout << "Enter Shop ID: ";
    cin >> shop.shopId;

    cin.ignore(); 
    cout << "Enter Shop Name: ";
    cin>>shop.shopName;

    fout << shop.shopId << " " << shop.shopName << endl;
    fout.close();
}

void viewShopRecords() {
    ifstream fin("ShopRecords.txt");
    Shop shop;

    cout << "Shop Records\n";
    cout << "ID\tName\n";
    while (fin >> shop.shopId>> shop.shopName) {
        cout << shop.shopId << "\t" << shop.shopName << endl;
    }
    fin.close();
}

void updateShop() {
    ifstream fin("ShopRecords.txt");
    ofstream fout("Temp.txt");
    Shop shop;
    int updateId;

    cout << "Enter Shop ID to update: ";
    cin >> updateId;

    bool found = false;
    while (fin >> shop.shopId>> shop.shopName) {
        if (shop.shopId == updateId) {
            found = true;
            cout << "Enter updated details:\n";
            cout << "New Name: ";
            getline(cin, shop.shopName);
            fout << shop.shopId << " " << shop.shopName << endl;
            cout << "Record updated successfully!\n";
        }
        else {
            fout << shop.shopId << " " << shop.shopName << endl;
        }
    }

    if (!found) {
        cout << "Shop not found!\n";
    }

    fin.close();
    fout.close();
    remove("ShopRecords.txt");
    rename("Temp.txt", "ShopRecords.txt");
}

void shopRegistration() {
    int shopId;
    string shopType;

    cout << "Enter Shop ID to register: ";
    cin >> shopId;
    cout << "Enter Shop Type: ";
    cin >> shopType;

    ifstream fin("ShopRecords.txt");
    Registration reg;

    while (fin >> reg.shopId >> reg.shopType) {
        if (shopId == reg.shopId) {
            cout << "Shop already exist.";
            break;
        }
        else {
            ofstream fout("ShopRegistration.txt", ios::app);
            fout << shopId << " " << shopType << endl;
            fout.close();
        }
    }
    fin.close();
}


void viewRegistrations() {
    ifstream fin("ShopRegistration.txt");
    Registration reg;

    cout << "Shop Registrations\n";
    cout << "Shop ID\tShop Type\n";
    while (fin >> reg.shopId>> reg.shopType) {
        cout << reg.shopId << "\t" << reg.shopType << endl;
    }
    fin.close();
}

void exitSystem() {
    cout << "Exiting from the system...\n";
    exit(0);
}