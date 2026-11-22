Kunal CD 
1.   VS CODE VERSION


#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>

#define NUM 256
#define ID 257
#define DONE 0

char input[100];
char lexeme[100];
int pos = 0;
int token;

void lexer()
{
    int i = 0;

    while (isspace(input[pos]))
        pos++;

    if (isalpha(input[pos]))
    {
        while (isalnum(input[pos]))
            lexeme[i++] = input[pos++];

        lexeme[i] = '\0';
        token = ID;
    }
    else if (isdigit(input[pos]))
    {
        while (isdigit(input[pos]))
            lexeme[i++] = input[pos++];

        lexeme[i] = '\0';
        token = NUM;
    }
    else if (input[pos] == '\0')
    {
        token = DONE;
    }
    else
    {
        token = input[pos++];
    }
}

void error()
{
    printf("\nString Rejected\n");
    exit(0);
}

void Match(int t)
{
    if (token == t)
        lexer();
    else
        error();
}

void E();
void T();
void F();

void F()
{
    if (token == '(')
    {
        Match('(');
        E();
        Match(')');
    }
    else if (token == ID || token == NUM)
    {
        printf("%s ", lexeme);
        Match(token);
    }
    else
        error();
}

void T()
{
    int op;

    F();

    while (token == '*' || token == '/')
    {
        op = token;
        Match(op);
        F();
        printf("%c ", op);
    }
}

void E()
{
    int op;

    T();

    while (token == '+' || token == '-')
    {
        op = token;
        Match(op);
        T();
        printf("%c ", op);
    }
}

int main()
{
    printf("PROGRAM FOR RECURSIVE DESCENT PREDICTIVE PARSING\n");

    printf("\nEnter arithmetic expressions.");
    printf("\nUse semicolon (;) at the end of each expression.\n");
    printf("\nExample: a+b*c;\n");

    fgets(input, sizeof(input), stdin);

    lexer();

    while (token != DONE)
    {
        printf("\nPostfix Expression: ");

        E();

        Match(';');

        printf("\nExpression successfully parsed.\n");
    }

    printf("\nParsing completed.\n");

    return 0;
}


## Compile:
gcc predictive.c -o predictive
.\predictive.exe










KUNAL CD
2.  TURBO C VERSION


#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>

#define NUM 256
#define ID 257
#define DONE 0

char input[100];
char lexeme[100];
int pos = 0;
int token;

void lexer()
{
    int i = 0;

    while (isspace(input[pos]))
        pos++;

    if (isalpha(input[pos]))
    {
        while (isalnum(input[pos]))
            lexeme[i++] = input[pos++];

        lexeme[i] = '\0';
        token = ID;
    }
    else if (isdigit(input[pos]))
    {
        while (isdigit(input[pos]))
            lexeme[i++] = input[pos++];

        lexeme[i] = '\0';
        token = NUM;
    }
    else if (input[pos] == '\0')
    {
        token = DONE;
    }
    else
    {
        token = input[pos++];
    }
}

void error()
{
    printf("\nString Rejected\n");
    exit(0);
}

void Match(int t)
{
    if (token == t)
        lexer();
    else
        error();
}

void E();
void T();
void F();

void F()
{
    if (token == '(')
    {
        Match('(');
        E();
        Match(')');
    }
    else if (token == ID || token == NUM)
    {
        printf("%s ", lexeme);
        Match(token);
    }
    else
        error();
}

void T()
{
    int op;

    F();

    while (token == '*' || token == '/')
    {
        op = token;
        Match(op);
        F();
        printf("%c ", op);
    }
}

void E()
{
    int op;

    T();

    while (token == '+' || token == '-')
    {
        op = token;
        Match(op);
        T();
        printf("%c ", op);
    }
}

int main()
{
    printf("PROGRAM FOR RECURSIVE DESCENT PREDICTIVE PARSING\n");

    printf("\nEnter arithmetic expressions.");
    printf("\nUse semicolon (;) at the end of each expression.\n");
    printf("\nExample: a+b*c;\n");

    gets(input);

    lexer();

    while (token != DONE)
    {
        printf("\nPostfix Expression: ");

        E();

        Match(';');

        printf("\nExpression successfully parsed.\n");
    }

    printf("\nParsing completed.\n");

    getch();
    return 0;
}















1.OM ATL 
#code 
library(shiny)

ui <- fluidPage(
  
  titlePanel("My First Shiny App"),
  
  sidebarLayout(
    position = "right",
    
    sidebarPanel(
      "This is the Sidebar Panel"
    ),
    
    mainPanel(
      "This is the Main Panel"
    )
  )
)

server <- function(input, output) {
  
}

shinyApp(ui = ui, server = server)



#Console command 
install.packages("shiny")
library(shiny)
