# -inventory-management
 inventory management system for a fictional retail store. 

#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Product {
public:
    Product(string name, float price, int quantity) : name(name), price(price), quantity(quantity) {}

    string getName() const {
        return name;
    }

    float getPrice() const {
        return price;
    }

    int getQuantity() const {
        return quantity;
    }

    void setQuantity(int newQuantity) {
        quantity = newQuantity;
    }

private:
    string name;
    float price;
    int quantity;
};

class Inventory {
public:
    void addProduct(const Product& product) {
        products.push_back(product);
    }

    bool removeProduct(const string& productName) {
        for (auto it = products.begin(); it != products.end(); ++it) {
            if (it->getName() == productName) {
                products.erase(it);
                return true;
            }
        }
        return false;
    }

    bool updateQuantity(const string& productName, int newQuantity) {
        for (auto& product : products) {
            if (product.getName() == productName) {
                product.setQuantity(newQuantity);
                return true;
            }
        }
        return false;
    }

    void displayInventory() const {
        cout << "Current Inventory:" << endl;
        for (const auto& product : products) {
            cout << "Product: " << product.getName() << ", Price: $" << product.getPrice() << ", Quantity: " << product.getQuantity() << endl;
        }
    }

private:
    vector<Product> products;
};

int main() {
    Inventory inventory;

    // Adding some initial products
    inventory.addProduct(Product("Shirt", 20.00, 50));
    inventory.addProduct(Product("Pants", 30.00, 30));
    inventory.addProduct(Product("Shoes", 50.00, 20));

    while (true) {
        cout << "\nOptions:" << endl;
        cout << "1. Add Product" << endl;
        cout << "2. Remove Product" << endl;
        cout << "3. Update Quantity" << endl;
        cout << "4. Display Inventory" << endl;
        cout << "5. Exit" << endl;

        int choice;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: {
                string name;
                float price;
                int quantity;
                cout << "Enter product name: ";
                cin >> name;
                cout << "Enter product price: ";
                cin >> price;
                cout << "Enter product quantity: ";
                cin >> quantity;
                inventory.addProduct(Product(name, price, quantity));
                break;
            }
            case 2: {
                string name;
                cout << "Enter product name to remove: ";
                cin >> name;
                if (!inventory.removeProduct(name)) {
                    cout << "Product not found in inventory." << endl;
                }
                break;
            }
            case 3: {
                string name;
                int newQuantity;
                cout << "Enter product name to update quantity: ";
                cin >> name;
                cout << "Enter new quantity: ";
                cin >> newQuantity;
                if (!inventory.updateQuantity(name, newQuantity)) {
                    cout << "Product not found in inventory." << endl;
                }
                break;
            }
            case 4:
                inventory.displayInventory();
                break;
            case 5:
                cout << "Exiting program." << endl;
                return 0;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    }

    return 0;
}
