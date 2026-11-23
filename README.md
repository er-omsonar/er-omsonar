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
