#include <iostream>
#include <string>
#include <vector>
#include <tuple>
#include <unordered_map>
#include <climits>
#include <algorithm>

using namespace std;

void gatherUserInfo();

void gatherDisasterInfo();

void sendImmediateHelp();

unordered_map<string, string> userInfo;

vector<tuple<string, string, int>> disasterInfo;

int main() {

    cout << "****************" << endl;
    cout << "*                                        *" << endl;
    cout << "*          DISASTER RESPONSE SYSTEM      *" << endl;
    cout << "*                                        *" << endl;
    cout << "****************" << endl;

    int choice;

    do {
        cout << "\nMenu:\n";
        cout << "1. Enter User Information\n";
        cout << "2. Enter Disaster Information\n";
        cout << "3. Send Immediate Help\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                gatherUserInfo();
                break;
            case 2:
                gatherDisasterInfo();
                break;
            case 3:
                sendImmediateHelp();
                break;
            case 4:
                cout << "Exiting the system.\n";
                break;
            default:
                cout << "Invalid choice. Please try again.\n";
                break;
        }

    } while (choice != 4);

    return 0;

}

void gatherUserInfo() {

    string name, contact, location;

    cout << "Enter your name: ";
    cin.ignore(); // To clear the buffer
    getline(cin, name);

    cout << "Enter your contact information: ";
    getline(cin, contact);

    cout << "Enter your current location: ";
    getline(cin, location);

    // Store the user information in the unordered_map
    userInfo["name"] = name;
    userInfo["contact"] = contact;
    userInfo["location"] = location;

    cout << "User information saved successfully.\n";

}

void gatherDisasterInfo() {

    int numDisasters;

    cout << "Enter the number of disaster occurrences in your area: ";
    cin >> numDisasters;

    disasterInfo.clear();

    for (int i = 0; i < numDisasters; ++i) {

        string city, disasterType;
        int threatLevel;

        cout << "Disaster " << i + 1 << ":\n";
        cout << "City: ";
        cin >> city;

        cout << "Disaster Type: ";
        cin >> disasterType;

        cout << "Threat Level (1-10): ";
        cin >> threatLevel;

        disasterInfo.push_back(make_tuple(city, disasterType, threatLevel));
    }

    cout << "Disaster information saved successfully.\n";

}

void sendImmediateHelp() {

    if (userInfo.empty() || disasterInfo.empty()) {
        cout << "Please enter user information and disaster information first.\n";
        return;
    }

    string name = userInfo["name"];
    string contact = userInfo["contact"];
    string location = userInfo["location"];

    cout << "Sending immediate help to " << name << " at " << location << ".\n";

    cout << "Contacting emergency services...\n";

    cout << "Help is on the way. Stay safe!\n";

}
