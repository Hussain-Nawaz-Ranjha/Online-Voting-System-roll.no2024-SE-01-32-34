//                                                         ROLL NO 1, 32 AND 34 PROJECT
#include<iostream>
#include<string>
#include<algorithm>
#include<fstream>
#include<iomanip>
using namespace std;

bool de = false;
bool le = false;
int tv = 0;
int votes = 0;
int tlc = 0;
int tdc = 0;
bool can = false;
int v = 0;
bool s = false;
string cnnicarr[100];
void loadlocalcand();
void loaddistcand();
void loadde();
void loadle();
void loads();
void loadcnnic();

bool isValidCnic(const string& cnic) {
    return cnic.length() == 13 && all_of(cnic.begin(), cnic.end(), ::isdigit);
}
bool isValidName(const string& cnic) {
    return  all_of(cnic.begin(), cnic.end(), ::isalpha);
}

class user {
protected:
    string username;
    string password;
    string cnnic;
public:

    user() {
        username = "admin";
        password = "2024282e";
    }
    user(string u, string pass) {
        username = u;
        password = pass;
    }

    void setusername(string u) {
        username = u;
    }
    void setpassword(string p) {
        password = p;
    }
    void setcnnic(string c) {
        cnnic = c;
    }
    string getcnnic() {
        return cnnic;
    }
    string getusername() {
        return username;
    }
    string getpassword() {
        return password;
    }
    bool login(string n, string pass) {
        return (n == username && pass == password);
    }
};


class candidate {
protected:
    string username;
    string password;
    string cnnic;
    string party;
    int votes = 0;

public:
    candidate()
    {
        this->username = "name";
        this->cnnic = "cnic";
        this->password = "password";
        this->party = "party";
        this->votes = 0;
    }
    candidate(string name, string cnic, string password, string party, int votes)
    {
        this->username = name;
        this->cnnic = cnic;
        this->password = password;
        this->party = party;
        this->votes = votes;

    }

    static int totalvotes;

    void setusername(string username) {
        this->username = username;
    }
    void setpassword(string password) {
        this->password = password;
    }
    void setcnnic(string cnnic) {
        this->cnnic = cnnic;
    }
    void setparty(string par) {
        party = par;
    }
    void setvotes(int i) {
        this->votes += i;
    }
    void incrementVotes() {
        votes++;
    }
    string getusername() {
        return username;
    }
    string getpassword() {
        return password;
    }
    string getcnnic() {
        return cnnic;
    }
    string getparty() {
        return party;
    }

    int getvote() {
        return votes;
    }
    void getCandidateInfo() {
        cout << endl << username << " belongs to party: " << party << endl << " CNNIC: " << cnnic << endl << "Password: " << password << endl << " having votes: " << votes << endl << endl;
    }
};


candidate* candlocalArr = nullptr;
candidate* canddistArr = nullptr;
class voter : public user {
public:
    bool dcasted = false;
    bool lcasted = false;
    voter() {
        this->username = "name";
        this->cnnic = "cnnic";
        this->password = "password";
        this->dcasted = false;
        this->lcasted = false;
    }
    voter(string name, string cnnic, string password, bool dcasted, bool lcasted) {
        this->username = name;
        this->cnnic = cnnic;
        this->password = password;
        this->dcasted = dcasted;
        this->lcasted = lcasted;
    }

    string getcnic() {
        return cnnic;
    }
    void setdistcasted(bool flag) {
        this->dcasted = flag;
    }
    void setdlocalcasted(bool flag) {
        this->lcasted = flag;
    }
    bool getdistcasted() {
        return dcasted;
    }
    bool getlocalcasted() {
        return lcasted;
    }
    void castvote() {
        loadde();
        loadle();
        loaddistcand();
        loadlocalcand();
        int choice;

        if (candlocalArr == nullptr || tdc == 0 || canddistArr == nullptr || candlocalArr == nullptr) {
            cout << "No candidates available.\n";
            return;
        }
        cout << "To whom you want to cast vote:\n";
        if (de == true) {
            for (int i = 0; i < tdc - 1; i++) {
                cout << "Press " << i + 1 << " to cast vote to ";
                cout << canddistArr[i].getusername();
                cout << " (Party: " << canddistArr[i].getparty() << ")\n";
            }
        }
        else if (le == true) {
            for (int i = 0; i < tlc; i++) {
                cout << "Press " << i + 1 << " to cast vote to ";
                cout << candlocalArr[i].getusername();
                cout << " (Party: " << candlocalArr[i].getparty() << ")\n";
            }
        }

        cin >> choice;
        if (choice >= 1 && choice <= tdc && de == true) {
            canddistArr[choice - 1].incrementVotes();
            ofstream outfile("DistCandidate.txt");
            for (int i = 0; i < tdc - 1; i++) {
                if (outfile.is_open()) {
                    outfile << canddistArr[i].getusername() << "\t" << canddistArr[i].getcnnic() << "\t" << canddistArr[i].getpassword() << "\t" << canddistArr[i].getparty() << "\t" << canddistArr[i].getvote() << endl;
                }
                else {
                    cout << "Error opening file!" << endl;
                }
            }
            outfile.close();
            cout << "\nVote casted successfully!\n";
            return;
        }
        else if (choice >= 1 && choice <= tlc && le == true) {
            candlocalArr[choice - 1].incrementVotes();
            lcasted = true;
            ofstream outf("localCandidate.txt");
            for (int i = 0; i < tdc - 1; i++) {

                if (outf.is_open()) {
                    outf << candlocalArr[i].getusername() << "\t" << candlocalArr[i].getcnnic() << "\t" << candlocalArr[i].getpassword() << "\t" << candlocalArr[i].getparty() << "\t" << candlocalArr[i].getvote() << endl;
                }
                else {
                    cout << "Error opening file!" << endl;
                }

            }
            outf.close();
            cout << "\nVote casted successfully!\n";
            return;
        }
        else {
            cout << "Invalid choice.\n";
        }
    }
    void checkvotestatus() {
        if (de == true && dcasted == true) {
            cout << endl << "Your district vote has been casted successfully" << endl << endl << endl;
        }
        else if (le == true && lcasted == true) {
            cout << endl << "Your local vote has been casted successfully" << endl << endl << endl;
        }
        else
            cout << endl << "Your vote is yet to caste" << endl << endl << endl;
    }
    void getVoterInfo() {
        cout << endl << "Username: " << username << endl << " CNNIC: " << cnnic << endl << "Password: " << password << endl;
    }
};
voter* voterArr = nullptr;
void loadvoter() {
    voterArr = nullptr;
    string name, cnnic, password;
    bool dcasted, lcasted;
    ifstream infile("Voter.txt");
    voterArr = new voter[100];
    int i = 0;

    while (!infile.eof())
    {
        infile >> name >> cnnic >> password >> boolalpha >> dcasted >> boolalpha >> lcasted;
        voterArr[i] = voter(name, cnnic, password, dcasted, lcasted);
        i++;
    }
    tv = i;
    infile.close();
}
class election {
public:
    bool flag = true;
    bool bcnnic = true;
    int check;
    int c = 0;
    string cnnic;
    string p;
    string par;
    voter v;

    void endelection() {
        if (s == false)
            cout << "\nElection has not Started yet\n";
        else if (s == true) {
            s = false;
            cout << "\nElection has ended\n";
        }
    }

    void addvoter() {
        loadvoter();
        string u;
        if (s == false) {
            cout << "How many voters you want to add: ";
            cin >> c;
            if (c > 0)
                can = true;

            voterArr = new voter[c + tv];
            ofstream outfile("Voter.txt", ios::app);
            if (outfile.is_open()) {
                for (int i = tv; i < tv + c; i++) {

                    cout << "Enter name of voter " << i + 1 << ": ";
                    getline(cin, u);
                    getline(cin, u);
                    while (u.empty()) {
                        cout << "Name of voter can't be empty\nRe-enter the name: ";
                        getline(cin, u);
                    }
                    while (!isValidName(u)) {
                        cout << "\nName of voter can't be in digits\nre-enter the name\n";
                        getline(cin, u);
                    }
                    voterArr[i].setusername(u);
                    do {
                        cout << "Enter CNIC without spaces: ";
                        getline(cin, cnnic);
                        if (!isValidCnic(cnnic)) {
                            cout << "Invalid CNIC. Must be 13 digits.\n";
                        }
                    } while (!isValidCnic(cnnic));
                    /*  a:
                      for (int j = 0; j < tv; j++) {
                          if (voterArr[j].getcnic() == cnnic) {
                              cout << "Cnnic can't be similar to others\nRe-enter cnnic\n";
                              getline(cin, cnnic);
                              goto a;
                          }
                      }*/
                    cout << "CNIC VERIFIED\n";

                    bool cnnicflag = true;
                    while (cnnicflag) {
                        if (cnnic.substr(0, 3) == "344") {
                            cout << "Voter authorized\n";
                            cnnicflag = false;
                        }
                        else {
                            cout << "Enter CNIC starting with 344: ";
                            getline(cin, cnnic);
                        }
                    }
                    voterArr[i].setcnnic(cnnic);
                    cout << "Enter password for voter " << i + 1 << ": ";
                    cin >> p;
                    voterArr[i].setpassword(p);
                    voterArr[i].setdistcasted(false);
                    voterArr[i].setdlocalcasted(false);
                    outfile << voterArr[i].getusername() << "\t" << voterArr[i].getcnnic() << "\t" << voterArr[i].getpassword() << "\t" << boolalpha << voterArr[i].getdistcasted() << "\t" << boolalpha << voterArr[i].getlocalcasted() << endl;
                    outfile.close();
                    cout << "\nVoter added successfully.\n";
                }
            }
            else {
                cout << "Error opening file!" << endl;
            }
            tv += 1;

        }
        else {
            cout << "Election has not started.\n";
        }
    }
    virtual void showcandidate() {
        loadde();
        loadle();
        loaddistcand();
        loadlocalcand();
        if (de == true) {
            for (int i = 0; i < tdc; i++) {
                canddistArr[i].getCandidateInfo();
            }
        }
        else if (le == true) {
            for (int i = 0; i < tlc; i++) {
                candlocalArr[i].getCandidateInfo();
            }
        }
    }
};
class localelection :public election {
public:
    bool flag = true;
    int check;
    int c = 0;
    string cnnic;
    string p;
    string par;
    void addcandidate() {
        loadlocalcand();
        string u = "abc";
        if (s == false) {
            cout << "\nHow many candidates you want to add: ";
            cin >> c;
            if (c > 0)
                can = true;
            candlocalArr = new candidate[c + tlc];
            ofstream outfile("localCandidate.txt", ios::app);
            if (outfile.is_open()) {
                for (int i = tlc; i < tlc + c; i++) {

                    cout << "Enter name of candidate " << i + 1 << ": ";
                    getline(cin, u);///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
                    getline(cin, u);
                    while (u.empty() && isValidName(u)) {
                        cout << "\nName of candidate can't be empty\nre-enter the name\n";
                        getline(cin, u);
                    }
                    while (!isValidName(u)) {
                        cout << "\nName of candidate can't be in digits\nre-enter the name\n";
                        getline(cin, u);
                    }

                    candlocalArr[i].setusername(u);

                    do {
                        cout << "Enter CNIC without spaces: ";
                        getline(cin, cnnic);
                        if (!isValidCnic(cnnic)) {
                            cout << "Invalid CNIC. Must be 13 digits.\n";
                        }
                    } while (!isValidCnic(cnnic));

                    cout << "CNIC VERIFIED\n";

                    bool cnnicflag = true;
                    while (cnnicflag) {
                        if (cnnic.substr(0, 3) == "344") {
                            cout << "Candidate authorized\n";
                            cnnicflag = false;
                        }
                        else {
                            cout << "Enter CNIC starting with 344: ";
                            getline(cin, cnnic);
                        }
                    }
                    candlocalArr[i].setcnnic(cnnic);

                    cout << "Enter password for candidate " << i + 1 << ": ";
                    cin >> p;
                    candlocalArr[i].setpassword(p);

                    cout << "Enter party name: ";
                    cin.ignore();
                    getline(cin, par);
                    while (par.empty()) {
                        cout << "Name of party can't be empty\nRe-enter the name of party: ";
                        getline(cin, par);
                    }
                    candlocalArr[i].setvotes(0);
                    candlocalArr[i].setparty(par);
                    outfile << candlocalArr[i].getusername() << "\t" << candlocalArr[i].getcnnic() << "\t" << candlocalArr[i].getpassword() << "\t" << candlocalArr[i].getparty() << "\t" << candlocalArr[i].getvote() << endl;
                    cout << "\nCandidate added successfully\n";
                }
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outfile.close();
            tlc += c;
        }
        else {
            cout << "\nElection has not started\n";
        }
    }
    void endlocalelection() {
        if (le == false)
            cout << "\nLocal Election has not Started yet\n";
        else if (le == true) {
            s = false;
            le = false;
            fstream outfile("le.txt", ios::app);
            if (outfile.is_open()) {
                outfile << boolalpha << le;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outfile.close();
            fstream outf("s.txt", ios::app);
            if (outf.is_open()) {
                outf << boolalpha << s;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outf.close();
            cout << "\nElection has ended\n";
        }
    }

    void startlocalelection() {
        if (de == true) {
            cout << "\nDistrict Election is under waay can't start local elections now\n";
            return;
        }
        else if (le == true) {
            cout << "\nLocal Election is already underway\n";
        }
        else {
            s = true;
            le = true;
            fstream outfile("le.txt", ios::app);
            if (outfile.is_open()) {
                outfile << boolalpha << le;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outfile.close();
            fstream outf("s.txt", ios::app);
            if (outf.is_open()) {
                outf << boolalpha << s;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outf.close();
            cout << "\nLocal election has started\n";
        }

    }
    void showcandidate() {
        loadle();
        loadlocalcand();
        if (le == true) {
            for (int i = 0; i < tlc; i++) {
                candlocalArr[i].getCandidateInfo();
            }
        }
        else {
            cout << "local election has not started";
            return;
        }
    }
};
class districtelection :public election {
public:
    bool flag = true;
    int check;
    int c = 0;
    string cnnic;
    string p;
    string par;
    void adddistcandidate() {
        loaddistcand();
        string u = "abc";
        if (s == false) {
            cout << "\nHow many candidates you want to add: ";
            cin >> c;
            if (c > 0)
                can = true;
            canddistArr = new candidate[c + tdc];
            ofstream outfile("DistCandidate.txt", ios::app);
            if (outfile.is_open()) {
                for (int i = tdc; i < tdc + c; i++) {

                    cout << "Enter name of candidate " << i + 1 << ": ";
                    getline(cin, u);///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
                    getline(cin, u);
                    while (u.empty() && isValidName(u)) {
                        cout << "\nName of candidate can't be empty\nre-enter the name\n";
                        getline(cin, u);
                    }
                    while (!isValidName(u)) {
                        cout << "\nName of candidate can't be in digits\nre-enter the name\n";
                        getline(cin, u);
                    }
                    canddistArr[i].setusername(u);
                    do {
                        cout << "Enter CNIC without spaces: ";
                        getline(cin, cnnic);
                        if (!isValidCnic(cnnic)) {
                            cout << "Invalid CNIC. Must be 13 digits.\n";
                        }
                    } while (!isValidCnic(cnnic));
                    cout << "CNIC VERIFIED\n";
                    bool cnnicflag = true;
                    while (cnnicflag) {
                        if (cnnic.substr(0, 3) == "344") {
                            cout << "Candidate authorized\n";
                            cnnicflag = false;
                        }
                        else {
                            cout << "Enter CNIC starting with 344: ";
                            getline(cin, cnnic);
                        }
                    }
                    canddistArr[i].setcnnic(cnnic);

                    cout << "Enter password for candidate " << i + 1 << ": ";
                    cin >> p;
                    canddistArr[i].setpassword(p);

                    cout << "Enter party name: ";
                    cin.ignore();
                    getline(cin, par);
                    while (par.empty()) {
                        cout << "Name of party can't be empty\nRe-enter the name of party: ";
                        getline(cin, par);
                    }
                    canddistArr[i].setparty(par);
                    canddistArr[i].setvotes(0);
                    outfile << canddistArr[i].getusername() << "\t" << canddistArr[i].getcnnic() << "\t" << canddistArr[i].getpassword() << "\t" << canddistArr[i].getparty() << "\t" << canddistArr[i].getvote() << endl;
                    cout << "\nCandidate added successfully\n";
                }
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outfile.close();
            tdc += c;

        }
        else {
            cout << "\nElection has not started\n";
        }
    }

    void enddisttelection() {

        if (de == false)
            cout << "\nDistrict Election has not Started yet\n";
        else if (de == true) {
            s = false;
            de = false;
            fstream outfile("de.txt", ios::app);
            if (outfile.is_open()) {
                outfile << boolalpha << de;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outfile.close();
            fstream outf("s.txt", ios::app);
            if (outf.is_open()) {
                outf << boolalpha << s;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outf.close();

            cout << "\nElection has ended\n";
        }
    }

    void startdistelection() {

        if (de == true) {
            cout << "\nDistrict Election has already started\n";
        }

        else {
            s = true;
            de = true;
            fstream outfile("de.txt", ios::app);
            if (outfile.is_open()) {
                outfile << boolalpha << de;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outfile.close();
            fstream outf("s.txt", ios::app);
            if (outf.is_open()) {
                outf << boolalpha << s;
            }
            else {
                cout << "Error opening file!" << endl;
            }
            outf.close();
            cout << "\nDistrict Election has started\n";
        }
    }
    void showcandidate() {
        loadde();
        loaddistcand();
        if (de == true) {
            for (int i = 0; i < tdc; i++) {
                canddistArr[i].getCandidateInfo();
            }

        }
        else {
            cout << "district election has not started";
            return;
        }
    }
};
void loadcnnic() {
    string cnnic;

    ifstream infile("cnnic.txt");
    int i = 0;
    while (!infile.eof())
    {
        infile >> cnnic;
        cnnicarr[i] = cnnic;
        i++;
    }

    infile.close();
    return;
}
void loads() {
    bool flag = false;
    ifstream infile("s.txt");
    while (!infile.eof())
    {
        infile >> boolalpha >> flag;
    }
    s = flag;
    infile.close();
    return;
}
void loadde() {
    bool flag = false;
    ifstream infile("de.txt");
    int i = 0;
    while (!infile.eof())
    {
        infile >> boolalpha >> flag;
        i++;
    }
    de = flag;
    infile.close();
    return;
}
void loadle() {
    bool flag = false;
    ifstream infile("le.txt");
    int i = 0;
    while (!infile.eof())
    {
        infile >> boolalpha >> flag;
        i++;
    }
    le = flag;
    infile.close();
    return;
}

void loaddistcand() {
    canddistArr = nullptr;
    string name, cnic, password, party;
    int votes;
    ifstream infile("DistCandidate.txt");
    canddistArr = new candidate[100];
    int i = 0;

    while (!infile.eof())
    {
        infile >> name >> cnic >> password >> party >> votes;
        canddistArr[i] = candidate(name, cnic, password, party, votes);
        i++;
    }
    tdc = i;
    infile.close();
    return;
}
void loadlocalcand() {
    candlocalArr = nullptr;
    string name, cnic, password, party;
    int votes;
    ifstream infile("localCandidate.txt");
    candlocalArr = new candidate[100];
    int i = 0;
    while (!infile.eof())
    {
        infile >> name >> cnic >> password >> party >> votes;
        candlocalArr[i] = candidate(name, cnic, password, party, votes);
        i++;
        tlc = i;
    }
    infile.close();

}
class administrator : public user, public localelection, public districtelection {
public:

    void createElection() {
        s = true;
    }

    void viewResults() {

        loaddistcand();
        loadlocalcand();
        if (candlocalArr == nullptr || tlc == 0 || canddistArr == nullptr || tdc == 0) {
            cout << "No candidates available.\n";
            return;
        }
        else if (le == true) {
            for (int i = 0; i < tlc - 1; i++) {
                cout << endl << candlocalArr[i].getusername() << " has votes: ";
                cout << candlocalArr[i].getvote() << endl;
            }cout << endl << "\t**************GRAPH************** "; cout << endl;
            for (int i = 0; i < tlc - 1; i++) {
                cout << setw(10) << left << candlocalArr[i].getusername() << ": ";
                for (int j = 0; j < candlocalArr[i].getvote(); j++) {
                    cout << "*";
                }
                cout << endl;
            }
        }
        else if (de == true) {
            for (int i = 0; i < tdc - 1; i++) {
                cout << endl << canddistArr[i].getusername() << " has votes: ";
                cout << canddistArr[i].getvote() << endl;
            }cout << endl << "\t**************GRAPH************** "; cout << endl;
            for (int i = 0; i < tdc - 1; i++) {
                cout << setw(10) << left << canddistArr[i].getusername() << ": ";
                for (int j = 0; j < canddistArr[i].getvote(); j++) {
                    cout << "*";
                }
                cout << endl;
            }
        }
    }

    void viewcandidates() {
        loaddistcand();
        loadlocalcand();
        if (de == true) {
            loaddistcand();
            for (int i = 0; i < tdc - 1; i++) {
                canddistArr[i].getCandidateInfo();
            }
        }
        else if (le == true) {
            loadlocalcand();
            for (int i = 0; i < tlc - 1; i++) {
                candlocalArr[i].getCandidateInfo();
            }
        }
    }
    void viewvoter() {
        loadvoter();
        for (int i = 0; i < tv - 1; i++) {
            voterArr[i].getVoterInfo();
        }
    }
};
//functions
void admin();
void vote();
void menucandidate();

void menuadmin() {
    administrator adm;
    districtelection e;
    localelection el;
    int a = 0;
    string u;

    cout << "Press\n1. To add candidate\n2. To add voter\n3. To create election\n4. To view results\n5. To view candidates\n6. To view voters\n0.to Exit\n";
    cout << "Enter your command: ";
    cin >> a;

    if (a == 1) {
        if (s == true) {
            cout << "\nElection has started can't add candidate now\n";
            return;
        }

        else
        {
            int choice;
            cout << "\nwhich elecltion's candidate you want to add\nPress 1 for district candidate\nPress 2 to add local candidate\nEnter your choice: ";
            cin >> choice;
            if (choice == 1)
                e.adddistcandidate();
            else if (choice == 2)
                el.addcandidate();
            else {
                cout << "\nInvalid choice\n";
                return;
            }
        }
    }
    else if (a == 2) {
        if (s == true) {
            cout << "\nElection has started can't add voter now\n";
            return;
        }
        else;
        e.addvoter();
    }
    else if (a == 3) {
        int o;
        cout << "Press 1 to start district election\nPress 2 to start local election\nPress 3 to end elections\nEnter your command: ";
        cin >> o;
        switch (o) {
        case 1:
            e.startdistelection();
            break;
        case 2:
            el.startlocalelection();
            break;
        case 3:
            e.enddisttelection();
            el.endlocalelection();
            break;
        default:
            cout << "Invalid option.\n";
            break;
        }
    }
    else if (a == 4) {
        adm.viewResults();
    }
    else if (a == 5) {
        /* if (tlc == 0 && tdc == 0) {
             cout << "\nNo candidates avaiable\n\n";
         }*/
        adm.viewcandidates();
    }
    else if (a == 6) {
        if (tv == 0) {
            cout << "\nNo voters avaiable\n";
        }
        adm.viewvoter();
    }
    else if (a == 0)
        return;
    else {
        cout << "\nInvalid input.\n";
        return;

    }
}

/////////////////////////////                                          MAIN                                                   ////////////////////////////////////////       

int main() {
    loads();
    loadde();
    loadle();
    bool cancel = false;
    administrator adm;
    string username;
    string password;
    cout << "\t\t\t\t\tWELCOME TO ONLINE ELECTION SYSTEM\n\n\n";
    while (!cancel) {
        int a;
        cout << "\t\t\"Do You Want To Login\"\n";
        cout << "Press\n1.To Login as Administrator\n2.To Login as Candidate\n3.To Login as Voter\n0.To exit\nEnter your command: ";
        cin >> a;

        switch (a) {
        case 0:
            cancel = false;
            return 0;
        case 1: 
            cout << endl << "Enter your username: ";
            cin >> username;
            cout << endl << "Enter your password: ";
            cin >> password;
            if (username == "admin" && password == "202428")
                admin();
            else if (username != "admin" || password != "202428")
                cout << endl << "Invalid Information" << endl;
            break;
        case 2:
            menucandidate();
            break;
        case 3:
            vote();
            break;
        default:
            cancel = false;
            cout << "Invalid input.\nTry again\n";
            return 0;
        }
    }
    if (candlocalArr != nullptr) {
        delete[] candlocalArr;
    }
    if (canddistArr != nullptr) {
        delete[] canddistArr;
    }
    if (voterArr != nullptr) {
        delete[] voterArr;
    }
}

void admin() {
    bool cancel = true;
    int a;
    while (cancel) {

        menuadmin();

        cout << "Press 1. to continue or\nPress 0. to go back" << endl;
        cin >> a;
        if (a == 0) {
            cancel = false;
            cout << endl;
        }
        else if (a == 1) {
            cout << endl;
            cancel = true;
        }
    }
    return;
}

void vote() {
    loadvoter();
    bool flag = true;
    int func = 1;

    voter v;
    int choice;
    string cnnic;
    string pass;

    if (s == true) {
        cout << "\nPress\n1 to caste vote\n2 to view results\n3 to view vote status\n0 to go back\n";
        cout << "Enter your choice: ";
        cin >> choice; cout << endl;
        if (choice == 1) {
            cout << "Enter your CNIC: ";
            cin >> cnnic;
            cout << "Enter your password: ";
            cin >> pass;
            cout << endl;
            for (int i = 0; i < tv; i++)
            {
                if (voterArr[i].getcnnic() == cnnic && voterArr[i].getpassword() == pass) {
                    if (voterArr[i].getdistcasted() == true && de == true) {
                        cout << "\nYou have already casted District vote can't cast another vote\n\n";
                        return;
                    }
                    else if (voterArr[i].getlocalcasted() == true && le == true) {
                        cout << "\nYou have already casted Local vote can't cast another vote\n\n";
                        return;
                    }
                    else {
                        voterArr[i].castvote();
                        if (de == true) {

                            ofstream out("Voter.txt");
                            voterArr[i].setdistcasted(true);
                            for (int j = 0; j < tv; j++) {
                                if (out.is_open()) {
                                    out << voterArr[j].getusername() << "\t" << voterArr[j].getcnnic() << "\t" << voterArr[j].getpassword() << "\t" << boolalpha << voterArr[j].getdistcasted() << "\t" << boolalpha << voterArr[j].getlocalcasted() << endl;
                                }
                                else {
                                    cout << "Error opening file!" << endl;
                                }
                            }
                            out.close();
                            return;
                        }
                        else if (le == true) {

                            ofstream outf("Voter.txt");
                            voterArr[i].setdlocalcasted(true);
                            for (int j = 0; j < tv; j++) {
                                if (outf.is_open()) {
                                    outf << voterArr[j].getusername() << "\t" << voterArr[j].getcnnic() << "\t" << voterArr[j].getpassword() << "\t" << boolalpha << voterArr[j].getdistcasted() << "\t" << boolalpha << voterArr[j].getlocalcasted() << endl;
                                }
                                else {
                                    cout << "Error opening file!" << endl;
                                }
                            }
                            outf.close();
                            return;
                        }
                    }

                }
                else if (i == tv && voterArr[i].getcnnic() != cnnic && voterArr[i].getpassword() != pass) {
                    cout << "Invalid credentials.\n";
                }
            }
            return;
        }
        else if (choice == 2) {
            administrator admin;
            admin.viewResults();
        }
        else if (choice == 3) {
            cout << "Enter your CNIC: ";
            cin >> cnnic;
            cout << "Enter your password: ";
            cin >> pass;
            cout << endl;
            for (int i = 0; i < tv; i++) {
                if (voterArr[i].getcnnic() == cnnic && voterArr[i].getpassword() == pass)
                    voterArr[i].checkvotestatus();
            }
        }
        else if (choice == 0) {
            return;
        }

        else if (choice > 3) {
            cout << "\nInvalid input.\n";
            return;
        }

    }

    else if (s == false) {
        cout << "\nElection has not started yet\n";
        return;
    }
    else {
        cout << "\nInvalid input.\n";
        return;
    }

}

void menucandidate() {
    int choice;
    string cnnic;
    string pass;

    if (s == true) {
        cout << "\nPress\n1 to see your details\n2 to view results\n0 to go back\n";
        cout << "Enter your choice: ";
        cin >> choice; cout << endl;
        if (choice == 1) {
            cout << "Enter your CNIC: ";
            cin >> cnnic;
            cout << "Enter your password: ";
            cin >> pass;
            cout << endl;
            if (de == true) {
                loaddistcand();
                for (int i = 0; i < tdc; i++)
                {
                    if (canddistArr[i].getcnnic() == cnnic && canddistArr[i].getpassword() == pass) {

                        cout << endl; canddistArr[i].getCandidateInfo(); cout << endl;
                    }
                    else if (i == tdc && canddistArr[i].getcnnic() != cnnic && canddistArr[i].getpassword() != pass) {
                        cout << "Invalid credentials.\n";
                    }
                }
            }
            else if (le == true) {
                loadlocalcand();
                for (int i = 0; i < tlc; i++) {
                    if (candlocalArr[i].getcnnic() == cnnic && candlocalArr[i].getpassword() == pass) {

                        cout << endl; candlocalArr[i].getCandidateInfo(); cout << endl;
                    }
                    else if (i == tlc && candlocalArr[i].getcnnic() != cnnic && candlocalArr[i].getpassword() != pass) {
                        cout << "Invalid credentials.\n";
                    }
                }
            }
            return;
        }


        else if (choice == 2) {
            administrator admin;
            admin.viewResults();
        }
        else if (choice == 0) {
            return;
        }
        else if (choice > 2) {
            cout << "\nInvalid input.\n";
            return;
        }
        else if (s == false) {
            cout << "\nElection has not started yet\n";
            return;
        }
    }
    else {
        cout << "\nInvalid input.\n";
        return;
    }

}
