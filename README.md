# AICP-LAB-7
This is my Aicp Lab-7 Task

#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

const int NUM_CHARITIES = 3;

struct Charity {
    string name;
    int totalDonation;
};

void setupDonationSystem(Charity charities[]) {
    for (int i = 0; i < NUM_CHARITIES; ++i) {
        cout << "Enter the name of Charity " << i + 1 << ": ";
        cin >> charities[i].name;
    }

    cout << "Charities available for donation:" << endl;
    for (int i = 0; i < NUM_CHARITIES; ++i) {
        cout << i + 1 << ". " << charities[i].name << endl;
    }
}

void recordDonation(Charity charities[], int choice, double shoppingBill) {
    if (choice < 1 || choice > NUM_CHARITIES) {
        cout << "Invalid charity choice. Please choose a number between 1 and " << NUM_CHARITIES << "." << endl;
        return;
    }

    double donationAmount = shoppingBill * 0.01;
    charities[choice - 1].totalDonation += donationAmount;

    cout << "Donation of $" << fixed << setprecision(2) << donationAmount << " made to " << charities[choice - 1].name << "." << endl;
}

void showTotals(Charity charities[]) {
    cout << "Charity Totals:" << endl;
    
    for (int i = 0; i < NUM_CHARITIES - 1; ++i) {
        for (int j = 0; j < NUM_CHARITIES - i - 1; ++j) {
            if (charities[j].totalDonation < charities[j + 1].totalDonation) {
                swap(charities[j], charities[j + 1]);
            }
        }
    }

    int grandTotal = 0;
    for (int i = 0; i < NUM_CHARITIES; ++i) {
        cout << charities[i].name << ": $" << fixed << setprecision(2) << charities[i].totalDonation << endl;
        grandTotal += charities[i].totalDonation;
    }

    cout << "GRAND TOTAL DONATED TO CHARITY: $" << grandTotal << endl;
}

int main() {
    Charity charities[NUM_CHARITIES];
    setupDonationSystem(charities);

    int choice;
    double shoppingBill;

    while (true) {
        cout << "\nEnter the charity choice (1-" << NUM_CHARITIES << ", -1 to show totals): ";
        cin >> choice;

        if (choice == -1) {
            showTotals(charities);
            break;
        }

        cout << "Enter the shopping bill amount: $";
        cin >> shoppingBill;

        recordDonation(charities, choice, shoppingBill);
    }

    return 0;
}

