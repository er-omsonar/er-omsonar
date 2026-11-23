ATL  3

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt


data = {
    'Country': ['India', 'USA', 'Italy', 'Brazil', 'China', 'Spain'],
    'Confirmed': [1000, 2000, 1500, 1200, 800, 1300],
    'Deaths': [50, 100, 80, 60, 40, 50],
    'Recovered': [200, 500, 400, 300, 250, 200]
}


df = pd.DataFrame(data)

# Display dataset
print("COVID-19 Dataset:")
print(df)

# Data Analytics
df['Active'] = df['Confirmed'] - df['Deaths'] - df['Recovered']

print("\nCOVID-19 Analysis:")
print(df)

# Statistical Analysis using NumPy
cases = np.array(df['Confirmed'])

print("\nData Analysis:")
print("Maximum Cases:", np.max(cases))
print("Minimum Cases:", np.min(cases))
print("Mean Cases:", np.mean(cases))
print("Standard Deviation:", np.std(cases))

# Bar Chart
plt.figure(figsize=(8, 5))
plt.bar(df['Country'], df['Confirmed'])
plt.title("Country-wise Confirmed Cases")
plt.xlabel("Country")
plt.ylabel("Confirmed Cases")
plt.show()

# Line Chart
plt.figure(figsize=(8, 5))
plt.plot(df['Country'], df['Confirmed'], marker='o')
plt.title("COVID-19 Cases")
plt.xlabel("Country")
plt.ylabel("Confirmed Cases")
plt.grid()
plt.show()

# Pie Chart
plt.figure(figsize=(8, 5))
plt.pie(df['Confirmed'], labels=df['Country'], autopct='%1.1f%%')
plt.title("COVID-19 Cases Distribution")
plt.show()

# Histogram
plt.figure(figsize=(8, 5))
plt.hist(df['Confirmed'], bins=5)
plt.title("Distribution of COVID-19 Cases")
plt.xlabel("Confirmed Cases")
plt.ylabel("Frequency")
plt.show()

python -m pip install numpy pandas matplotlib
python -m pip install -- upgrade pip




















OM CD EXP 3



#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    char data;
    struct Node *left, *right;
} Node;

char s[100];
int i = 0;

Node* expression();
Node* term();
Node* factor();

Node* newNode(char c)
{
    Node *n = (Node*)malloc(sizeof(Node));
    n->data = c;
    n->left = n->right = NULL;
    return n;
}

/* operands and parentheses */
Node* factor()
{
    Node *n;

    if (s[i] == '(')
    {
        i++;
        n = expression();
        i++;
        return n;
    }

    n = newNode(s[i]);
    i++;
    return n;
}

/* * and / */
Node* term()
{
    Node *left = factor();

    while (s[i] == '*' || s[i] == '/')
    {
        char op = s[i++];
        Node *right = factor();
        Node *n = newNode(op);

        n->left = left;
        n->right = right;
        left = n;
    }

    return left;
}

/* + and - */
Node* expression()
{
    Node *left = term();

    while (s[i] == '+' || s[i] == '-')
    {
        char op = s[i++];
        Node *right = term();
        Node *n = newNode(op);

        n->left = left;
        n->right = right;
        left = n;
    }

    return left;
}

/* Print tree sideways */
void printTree(Node *root, int space)
{
    if (root == NULL)
        return;

    space += 5;

    printTree(root->right, space);

    printf("\n");
    for (int j = 5; j < space; j++)
        printf(" ");

    printf("%c\n", root->data);

    printTree(root->left, space);
}

void preorder(Node *root)
{
    if (root)
    {
        printf("%c ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

void inorder(Node *root)
{
    if (root)
    {
        inorder(root->left);
        printf("%c ", root->data);
        inorder(root->right);
    }
}

void postorder(Node *root)
{
    if (root)
    {
        postorder(root->left);
        postorder(root->right);
        printf("%c ", root->data);
    }
}

int main()
{
    Node *root;

    printf("Enter expression: ");
    scanf("%s", s);

    root = expression();

    printf("\nSyntax Tree:\n");
    printTree(root, 0);

    printf("\nPreorder: ");
    preorder(root);

    printf("\nInorder: ");
    inorder(root);

    printf("\nPostorder: ");
    postorder(root);

    return 0;
}
