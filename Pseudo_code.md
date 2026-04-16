#Pseudo Code

FUNCTION precedence(op):
    IF op == '+' OR op == '-': RETURN 1
    IF op == '*' OR op == '/': RETURN 2
    IF op == '^': RETURN 3
    RETURN -1

FUNCTION infixToPostfix(expression):
    CREATE empty stack for operators
    CREATE empty string for result
    FOR each character ch in expression:
        IF ch is operand:
            ADD ch to result
        ELSE IF ch is '(':
            PUSH ch to stack
        ELSE IF ch is ')':
            WHILE stack not empty AND top != '(':
                POP and ADD to result
            POP '(' from stack
        ELSE IF ch is operator:
            WHILE stack not empty AND precedence(top) >= precedence(ch):
                POP and ADD to result
            PUSH ch to stack
    WHILE stack not empty:
        POP and ADD to result
    RETURN result

FUNCTION infixToPrefix(expression):
    REVERSE expression
    SWAP '(' with ')' and vice versa
    postfix = infixToPostfix(modified expression)
    RETURN REVERSE(postfix)
