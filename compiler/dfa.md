# DFA ( (Deterministic Finite Automaton)



DFA( Deterministic Finite Automaton)는 유한한 상태를 갖고, 각 상태에서 입력을 받아 다음 상태로 전이되는 자동화 시스템입니다. 이러한 자동화는 이론적으로 혹은 실제적으로 컴퓨터과학에서 다양한 응용 분야에 사용됩니다.

DFA의 주요 구성 요소는 다음과 같습니다:

1. **유한한 상태 집합 (States)**: DFA는 한정된 개수의 상태를 가집니다. 각 상태는 자동화의 현재 위치를 나타냅니다.
2. **입력 알파벳 (Alphabet)**: 각 상태에서 허용되는 입력의 집합을 정의합니다. 이것은 자동화가 받아들일 수 있는 입력 문자의 유한한 집합입니다.
3. **전이 함수 (Transition Function)**: DFA의 핵심은 현재 상태와 입력에 따라 다음 상태로 이동하는 규칙입니다. 일반적으로 이는 상태와 입력의 쌍을 다음 상태로 매핑하는 함수로 표현됩니다.
4. **시작 상태 (Start State)**: DFA의 시작점은 자동화의 시작 상태입니다. 자동화는 항상 이 상태에서 시작합니다.
5. **종료 상태 또는 최종 상태 (Accepting or Final States)**: 이러한 상태는 자동화가 종료되었음을 나타냅니다. 일부 입력을 처리한 후에 이러한 상태에 도달하면 자동화는 입력을 수용하고 완료됩니다.

DFA는 입력 문자열을 받아들이거나 거부하는 데 사용됩니다. 자동화는 시작 상태에서 시작하여 각 입력 문자에 따라 전이 함수를 사용하여 상태를 변경하고, 문자열의 끝에 도달했을 때 자동화가 종료 상태에 도달하는지 확인합니다. 종료 상태에 도달하면 자동화는 문자열을 수락하고, 그렇지 않으면 거부합니다.



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