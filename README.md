OM CD EXP 3

#include <stdio.h>
#include <stdlib.h>

struct Node
{
    char data;
    struct Node *left;
    struct Node *right;
};

char expressionStr[100];
int pos = 0;

/* Create a new node */
struct Node* createNode(char data)
{
    struct Node *newNode;

    newNode = (struct Node*)malloc(sizeof(struct Node));

    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;

    return newNode;
}

/* Function declarations */
struct Node* expression();
struct Node* term();
struct Node* factor();

/* Handle + and - */
struct Node* expression()
{
    struct Node *left, *right, *newNode;

    left = term();

    while (expressionStr[pos] == '+' ||
           expressionStr[pos] == '-')
    {
        char op = expressionStr[pos];
        pos++;

        right = term();

        newNode = createNode(op);
        newNode->left = left;
        newNode->right = right;

        left = newNode;
    }

    return left;
}

/* Handle * and / */
struct Node* term()
{
    struct Node *left, *right, *newNode;

    left = factor();

    while (expressionStr[pos] == '*' ||
           expressionStr[pos] == '/')
    {
        char op = expressionStr[pos];
        pos++;

        right = factor();

        newNode = createNode(op);
        newNode->left = left;
        newNode->right = right;

        left = newNode;
    }

    return left;
}

/* Handle operands and parentheses */
struct Node* factor()
{
    struct Node *node;

    if (expressionStr[pos] == '(')
    {
        pos++;

        node = expression();

        pos++;          /* skip ')' */

        return node;
    }

    node = createNode(expressionStr[pos]);
    pos++;

    return node;
}

/* Preorder traversal */
void preorder(struct Node *root)
{
    if (root != NULL)
    {
        printf("%c ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

/* Inorder traversal */
void inorder(struct Node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%c ", root->data);
        inorder(root->right);
    }
}

/* Postorder traversal */
void postorder(struct Node *root)
{
    if (root != NULL)
    {
        postorder(root->left);
        postorder(root->right);
        printf("%c ", root->data);
    }
}

/* Display syntax tree */
void display(struct Node *root, int level)
{
    int i;

    if (root == NULL)
        return;

    /* Display right subtree */
    display(root->right, level + 1);

    /* Print spaces */
    for (i = 0; i < level; i++)
        printf("        ");

    printf("%c\n", root->data);

    /* Display left subtree */
    display(root->left, level + 1);
}

int main()
{
    struct Node *root;

    printf("Enter expression: ");
    scanf("%s", expressionStr);

    root = expression();

    printf("\nSyntax Tree:\n\n");

    display(root, 0);

    printf("\nPreorder: ");
    preorder(root);

    printf("\nInorder: ");
    inorder(root);

    printf("\nPostorder: ");
    postorder(root);

    printf("\n");

    return 0;
}
