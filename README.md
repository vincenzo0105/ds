#include<iostream>
#include<cstring>
using namespace std;

class Stack {
    char arr[50];
    int topIndex;

    public:
    Stack() {
        topIndex = -1;
    }

    bool empty() {
        return topIndex == -1;
    }

    void push(char ch) {
        if(topIndex<49) {
            arr[++topIndex] = ch;
        }
    }

    char pop() {
        if(!empty()) {
            return arr[topIndex--];
        }
        return '\0';
    }

    char getTop() {
        if(!empty()) {
            return arr[topIndex];
        }
        return '\0';
    }
};

int operatorCheck(char ch) {
    return (ch == '+' || ch == '-' || ch == '*' || ch == '%' || ch == '/' || ch == '^');
}

int priority(char ch) {
    if(ch == '(') return 0;
    if(ch == '+' || ch == '-') return 1;
    if(ch == '*' || ch == '/') return 2;
    if(ch == '^') return 3;
    return -1;    // in case of non operator
}

bool operand(char ch) {
    return !(operatorCheck(ch) || ch == '(' || ch == ')');
}

void infixToPostfix() {
    char infix[50];
    cout << "Enter the infix expression: ";
    cin >> infix;
    Stack s1;
    int i = 0;
    while(infix[i] != '\0') {
        char ch = infix[i++];
        if (operand(ch)) {
            cout << ch;
        }
        else {
            if(ch == '(') {
                s1.push();
            } else if(ch == ')') {
                while(s1.getTop != '(')
                {
                    cout << s1.pop();
                }
                s1.push(ch);
            } else {
                while(!s1.empty() && priority(s1.getTop()) >= priority(ch)) {
                    cout << s1.pop();
                }
                s1.push(ch);
            }
            }
        }
        while(!s1.empty()) {
            cout << s1.pop();
        }
        cout << endl;
    }

    void reverse(char* exp) {
        int n = strlen(exp);
        for(int i=0; i< n/2; i++) {
            swap(exp[i], exp[n-i-1]);
        }
    }

    void infixToPrefix() {
        char infix[50];
        cout << "Enter the infix expression: ";
        cin >> infix;

        reverse(infix);
        Stack s1;
        int i=0;
        int j=0;
        char prefix[50];

        while(infix[i] != '\0') {
            char ch = infix[i++];
            if (operand(ch)) {
                prefix[j++] = ch;
            
            } else {
                if(ch == ')') {
                    s1.push(ch);
                }
                else if (ch == '(') {
                        while (s1.getTop() != ')') {
                            prefix[j++] = s1.pop();
                        }
                        s1.pop();
                    } 
                    else {
                        while(!s1.empty() && priority(s1.getTop()) > priority(ch)) {
                            prefix[j++] = s1.pop();
                        }
                        s1.push(ch);
                    }
                }
            }
            while(!s1.empty()) {
                prefix[j++] = s1.pop();
            }
            prefix[j] = '\0';
            reverse(prefix);
            cout << "Prefix expression is: " << prefix << endl;
        }

        void prefixToPostfix() {
            char prefix[50];
            cout << "Enter the prefix expression: ";
            cin >> prefix;

            Stack s1;
            int length = strlen(prefix);
            for(int i = length - 1; i >= 0; i--) {
                char ch = prefix[i];
                if(operand(ch)) {
                    s1.push(ch);
                }
                else {
                    char op1 = s1.pop();
                    char op2 = s1.pop();
                    char temp = string(1, op1) + string(1, op2) + ch;
                    for(char c : temp) {
                        s1.push(c);
                    }
                }
            }
            cout << "Postfix expression is: ";
            while(!s1.empty()) {
                cout << s1.pop();
            }
            cout << endl;
        }

        void prefixToInfix() {
            char prefix[50];
            cout << "Enter the prefix expression: ";
            cin >> prefix;

            Stack s1;
            int length = strlen(prefix);
            for(int i = length - 1; i >= 0; i--) {
                char ch = prefix[i];
                if(operand(ch)) {
                    s1.push(ch);
                }
                else {
                    char op1 = s1.pop();
                    char op2 = s1.pop();
                    char temp = "(" + string(1, op1) + string(1, ch) + string(1, op2) + ")";
                    for(char c : temp) {
                        s1.push(c);
                    }
                }
            }
            cout << "Postfix expression is: ";
            while(!s1.empty()) {
                cout << s1.pop();
            }
            cout << endl;
        }

        void postfixToInfix() {
            char prefix[50];
            cout << "Enter the prefix expression: ";
            cin >> prefix;

            Stack s1;
            int length = strlen(prefix);
            for(int i = 0; i < length; i++) {
                char ch = prefix[i];
                if(operand(ch)) {
                    s1.push(ch);
                }
                else {
                    char op1 = s1.pop();
                    char op2 = s1.pop();
                    char temp = "(" + string(1, op1) + string(1, ch) + string(1, op2) + ")";
                    for(char c : temp) {
                        s1.push(c);
                    }
                }
            }
            cout << "Postfix expression is: ";
            while(!s1.empty()) {
                cout << s1.pop();
            }
            cout << endl;
        }

        void postfixToPrefix() {
            char prefix[50];
            cout << "Enter the prefix expression: ";
            cin >> prefix;

            Stack s1;
            int length = strlen(prefix);
            for(int i = 0; i < length; i++) {
                char ch = prefix[i];
                if(operand(ch)) {
                    s1.push(ch);
                }
                else {
                    char op1 = s1.pop();
                    char op2 = s1.pop();
                    char temp = string(1, ch) + string(1, op1) + string(1, op2);
                    for(char c : temp) {
                        s1.push(c);
                    }
                }
            }
            cout << "Postfix expression is: ";
            while(!s1.empty()) {
                cout << s1.pop();
            }
            cout << endl;
        }

        int main() {
            int choice;
            do {
                cout << "Menu:\n";
                cout << "1. Infix to Postfix\n";
                cout << "2. Infix to Prefix\n";
                cout << "3. Prefix to Postfix\n";
                cout << "4. Prefix to Infix\n";
                cout << "5. Postfix to Infix\n";
                cout << "6. Postfix to Prefix\n";
                cout << "7. Exit\n";
                cout << "Enter your choice: ";
                cin >> choice;
        
                switch (choice) {
                    case 1:
                        infixToPostfix();
                        break;
                    case 2:
                        infixToPrefix();
                        break;
                    case 3:
                        prefixToPostfix();
                        break;
                    case 4:
                        prefixToInfix();
                        break;
                    case 5:
                        postfixToInfix();
                        break;
                    case 6:
                        postfixToPrefix();
                        break;
                    case 7:
                        cout << "Exiting the program." << endl;
                        break;
                    default:
                        cout << "Invalid choice. Please try again." << endl;
                }
            } while (choice != 7);
            return 0;
        }

        
    

