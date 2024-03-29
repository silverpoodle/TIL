# DFA ( (Deterministic Finite Automaton)







<br/>

<br/>

## Table Driven

<br/>

<img src="https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240329225408669.png" alt="image-20240329225408669" style="zoom:50%;" />

<br/>

```c
#include <stdio.h>
#include <string.h>

typedef enum {
    p,
    q,
    r
} State;

typedef enum {
    ZERO,
    ONE
} Symbol;

State transition(State current, Symbol input) {
    static State table[3][2] = {
        {q, p},
        {r, p},
        {r, r}
    };

    return table[current][input];
}

const char* stateToString(State s) {
    switch (s) {
        case p:
            return "p";
        case q:
            return "q";
        case r:
            return "r";
        default:
            return "Unknown";
    }
}

void printTransition(State from, Symbol input, State to) {
    printf("d(%s, ", stateToString(from));
    switch (input) {
        case ZERO:
            printf("0");
            break;
        case ONE:
            printf("1");
            break;
        default:
            printf("Unknown");
    }
    printf(") = %s\n", stateToString(to));
}

int main() {

    while (1)
    {
        State startState;
        State currentState = p;
        Symbol inputSequence[100];
        int inputLength;
        
        inputLength = 0;
        Symbol input;

        while (1) {
            printf("Enter start state (p, q, r): ");
            char startStateChar;
            scanf(" %c", &startStateChar);
            if (startStateChar == 'p' || startStateChar == 'q' || startStateChar == 'r') {
                startState = startStateChar - 'p';
                currentState = startState;
                break;
            } else {
                printf("Invalid start state. Please enter 'p', 'q', or 'r'.\n");
            }
        }

        printf("INPUT => 0 or 1, end with 9 : \n");


        while (1) {
            scanf("%d", &input);
            if (input ==  9)
                break;
            if (input != 0 && input != 1) {
                printf("잘못된 입력입니다.\n");
                continue;
            }
            inputSequence[inputLength++] = input;
        }

        printf("Start: p\n");

        for (int i = 0; i < inputLength; ++i) {
            printTransition(currentState, inputSequence[i], transition(currentState, inputSequence[i]));
            currentState = transition(currentState, inputSequence[i]);
        }

        printf("Final: %s\n", stateToString(currentState));

        if (currentState == r) {
            printf("TRUE\n\n");
        } else {
            printf("FALSE\n\n");
        }
    }

    return 0;
}
```

<br/>