#include <iostream>
#include <cstring>
using namespace std;

class sll {
    struct node {
        int prn;
        char name[10];
        node *next;
    } *start;

public:
    sll() { start = NULL; }

    void create();
    void display();
    void insert_beginning(); // President
    void insert_end();       // Secretary
    void insert_mid();       // Members
    void del_beginning();
    void del_end();
    void del_mid();
    void compute();
    void concatenate(sll obj2);
};

void sll::create() {
    node *temp, *curr;
    int prn, ans;
    do {
        temp = new node;
        temp->next = NULL;

        cout << "Enter PRN number: ";
        cin >> temp->prn;

        cout << "Enter name: ";
        cin >> temp->name;

        if (start == NULL) {
            start = temp;
            curr = temp;
        } else {
            curr->next = temp;
            curr = temp;
        }

        cout << "Do you want to add a new node? (1 for yes): ";
        cin >> ans;

    } while (ans == 1);
}

void sll::display() {
    if (start == NULL) {
        cout << "Club is empty" << endl;
        return;
    }

    node *t = start;
    while (t != NULL) {
        cout << t->prn << " " << t->name << " -> ";
        t = t->next;
    }
    cout << "NULL" << endl;
}

void sll::insert_beginning() {
    node *temp = new node;
    temp->next = NULL;

    cout << "Enter PRN number: ";
    cin >> temp->prn;

    cout << "Enter name: ";
    cin >> temp->name;

    if (start == NULL) {
        start = temp;
    } else {
        temp->next = start;
        start = temp;
    }
}

void sll::insert_end() {
    node *temp = new node;
    temp->next = NULL;

    cout << "Enter PRN number: ";
    cin >> temp->prn;

    cout << "Enter name: ";
    cin >> temp->name;

    if (start == NULL) {
        start = temp;
    } else {
        node *last = start;
        while (last->next != NULL) {
            last = last->next;
        }
        last->next = temp;
    }
}

void sll::insert_mid() {
    int loc;
    cout << "\nEnter location after which you want to insert: ";
    cin >> loc;

    node *temp = new node;
    temp->next = NULL;

    cout << "Enter PRN number: ";
    cin >> temp->prn;

    cout << "Enter name: ";
    cin >> temp->name;

    node *curr = start;
    for (int i = 1; i < loc; i++) {
        curr = curr->next;
    }
    temp->next = curr->next;
    curr->next = temp;
}

void sll::del_beginning() {
    if (start == NULL) {
        cout << "\nClub is empty" << endl;
        return;
    }

    node *temp = start;
    start = start->next;

    cout << temp->prn << "\t first element deleted" << endl;
    delete temp;
}

void sll::del_end() {
    if (start == NULL) {
        cout << "\nClub is empty" << endl;
        return;
    }

    node *temp = start, *prev = NULL;
    while (temp->next != NULL) {
        prev = temp;
        temp = temp->next;
    }

    if (prev == NULL) {
        start = NULL;
    } else {
        prev->next = NULL;
    }

    cout << temp->prn << "\t last element deleted" << endl;
    delete temp;
}

void sll::del_mid() {
    int loc;
    cout << "\nEnter location of the node which you want to delete: ";
    cin >> loc;

    node *curr = start, *temp = NULL;
    for (int i = 1; i < loc; i++) {
        temp = curr;
        curr = curr->next;
    }
    temp->next = curr->next;

    cout << curr->prn << "\t has been deleted" << endl;
    delete curr;
}

void sll::compute() {
    int count = 0;
    node *temp = start;

    if (start == NULL) {
        cout << "\nClub is empty" << endl;
        return;
    }

    while (temp != NULL) {
        count++;
        temp = temp->next;
    }
    cout << "Total no of members are\t" << count << endl;
}

void sll::concatenate(sll obj2) {
    if (obj2.start == NULL) {
        cout << "\nList 2 is empty" << endl;
        return;
    }

    node *temp = start;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = obj2.start;

    cout << "\nAfter concatenation: ";
    display();
}

int main() {
    sll obj;
    int ch;

    do {
        cout << "\n1. Create\n2. Insert at beginning\n3. Insert at end\n4. Insert after position\n";
        cout << "5. Display list\n6. Delete first element\n7. Delete last element\n8. Delete Member\n";
        cout << "9. Find total No. of members\n10. Concatenate lists\n0. Exit\nEnter your choice: ";
        cin >> ch;

        switch (ch) {
        case 1:
            obj.create();
            obj.display();
            break;
        case 2:
            obj.insert_beginning();
            obj.display();
            break;
        case 3:
            obj.insert_end();
            obj.display();
            break;
        case 4:
            obj.insert_mid();
            obj.display();
            break;
        case 5:
            obj.display();
            break;
        case 6:
            obj.del_beginning();
            obj.display();
            break;
        case 7:
            obj.del_end();
            obj.display();
            break;
        case 8:
            obj.del_mid();
            obj.display();
            break;
        case 9:
            obj.compute();
            break;
        case 10: {
            sll obj2, obj3;
            cout << "\nList 1: " << endl;
            obj2.create();
            cout << "\nList 2: " << endl;
            obj3.create();
            obj2.concatenate(obj3);
            obj2.display();
            break;
        }
        case 0:
            cout << "\nEnd of program" << endl;
            break;
        default:
            cout << "Invalid choice!" << endl;
        }
    } while (ch != 0);

    return 0;
}
