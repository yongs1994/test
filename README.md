# test
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Student {
    char name[100];
    struct Student* next;
} Student;

// 새 학생 노드를 생성하는 함수
Student* createStudent(const char* name) {
    Student* newStudent = (Student*)malloc(sizeof(Student));
    strcpy(newStudent->name, name);
    newStudent->next = NULL;
    return newStudent;
}

// 연결 리스트의 끝에 학생 추가
void appendStudent(Student** head, const char* name) {
    Student* newStudent = createStudent(name);
    if (*head == NULL) {
        *head = newStudent;
    } else {
        Student* current = *head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newStudent;
    }

}

// 모든 학생의 이름 출력
void printStudents(Student* head) {
    Student* current = head;
    while (current != NULL) {
        printf("%s\\n", current->name);
        current = current->next;
    }
}

int main() {
    Student* head = NULL;

    char name[100];
    while (1) {
        printf("학생 이름 입력 (종료하려면 'end' 입력): ");
        scanf("%99s", name);
        if (strcmp(name, "end") == 0) {
            break;
        }
        appendStudent(&head, name);
    }

    printf("학생 명단:\\n");
    printStudents(head);

    // 메모리 해제
    Student* current = head;
    while (current != NULL) {
        Student* toFree = current;
        current = current->next;
        free(toFree);
    }

    return 0;
}
