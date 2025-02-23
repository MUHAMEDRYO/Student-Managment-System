# Student-Managment-System
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

 //Create a Structure for Students
 typedef struct etudiant
 {
     char name[30];
     char adresse[60];
     char class[5];
     float average;
     struct etudiant *suivant;
 }etudiant;

 etudiant *head = NULL;

// Function prototypes
void menu_system();
void add_student();
void display_students();
void search_student();
void update_informations();
void delete_student();
void free_all_students();

void menu_system(){
    int choice;

    while(1){
        system("clear");

        printf("Enter the number of the feature you want to proceed :\n");
        printf("1.Add a new student\n");
        printf("2.Display all student\n");
        printf("3.Search for a student by name\n");
        printf("4.Update a student's information\n");
        printf("5.Delete a studentt\n");
        printf("6.Exit the program\n");
        
        printf("Enter your choice :\n");
        scanf("%d ", &choice);

        switch (choice) {
            case 1:
                add_student();
                break;
            case 2:
                display_students();
                break;
            case 3:
                search_student();
                break;
            case 4:
                update_informations();
                break;
            case 5:
                delete_student();
                break;
            case 6:
                printf("Exiting program...\n");
                return;  
            default:
                printf("Invalid choice. Please try again.\n");
                break;
        }
    }
    
}

void add_student(){
    etudiant *p = (etudiant *)malloc(sizeof(etudiant));
    if (p == NULL){
        printf("Allocatation failed !\n");
        return;
    }


    printf("Enter the new student informations :\n");

    printf("name :\n");
    scanf("%s ",p->name);
    printf("adress :\n");
    scanf("%s ",p->adresse);
    printf("class :\n");
    scanf("%s ",p->class);   
    printf("average grade :\n");
    scanf("%f ",&p->average);

    p->suivant = NULL;
    
     if (head == NULL) {
        head = p;
    } else {
        etudiant *temp = head;
        while (temp->suivant != NULL) {
            temp = temp->suivant;
        }
        temp->suivant = p;
    }

    printf("Student added successfully!\n");




}
void display_students(){
    if (head == NULL) {
        printf("No students registered yet.\n");
        return;
    }
    etudiant *p = head;
    while (p != NULL)
    {
        printf("the student is: %s, adresse : %s, class : %s and average grade : %0.2f  \n" ,p->name,p->adresse,p->class,p->average);
        p = p->suivant;
    }
    
}
void search_student(){
    char name1[30];
    printf("Enter the name of student to search :\n");
    scanf("%s ",name1);

    etudiant *p = head;
    while(p != NULL){
        if(strcmp(p->name, name1) == 0){
            printf("This student goes by name : %s, adresse : %s, class : %s and average grade : %0.2f  \n" ,p->name,p->adresse,p->class,p->average);
            return;
        }
        else{
            p = p->suivant;
        }
    }
    printf("Student not found.\n");
}
void update_informations(){
    char name1[30];
    int nga;
    etudiant *p = head;

    printf("Enter the name of student to update their informations :\n");
    scanf("%s ",name1);
    while(p != NULL){
        if(strcmp(p->name, name1) == 0){
            while(1){
                printf("Choose the feature to update :\n 1 for name \n 2 for adress \n 3 for class \n 4 for average grade\n");
                printf("Type 5 if you want to exitthe program\n");
                scanf("%d ",&nga);
        
        
        
                switch (nga)
                {
                case 1:
                    printf("Enter the new name :\n");
                    scanf("%s ",p->name);
                    break;
                case 2:
                    printf("Enter the new adress :\n");
                    scanf("%s ",p->adresse);
                    break;
                case 3:
                    printf("Enter the new class :\n");
                    scanf("%s ",p->class);
                    break;
                case 4:
                    printf("Enter the new average grade :\n");
                    scanf("%0.2f ",p->average);
                    break;
                case 5:
                    return; 
                
                default:
                printf("Invalid choice. Please try again.\n");
                    break;
                }
            }
        
            
        }
        p = p->suivant;
        
    }
    printf("Student not found.\n");

}
void delete_student() {
    char name1[30];
    printf("Enter the name of the student to delete:\n");
    scanf("%s", name1);

    etudiant *current = head;
    etudiant *previous = NULL;

    while (current != NULL) {
        if (strcmp(current->name, name1) == 0) {
            if (previous == NULL) {
                head = current->suivant;
            } else {
                previous->suivant = current->suivant;
            }
            free(current);
            printf("Student successfully deleted.\n");
            return;
        }
        previous = current;
        current = current->suivant;
    }

    printf("Student not found.\n");
}
void free_all_students() {
    etudiant *temp;
    while (head != NULL) {
        temp = head;
        head = head->suivant;
        free(temp);
    }
}

int main(){
    
    //Display the menu
    printf("                                                            Student Managment System\n");
    menu_system();
    
    free_all_students();
    printf("Thank you for using the Student Management System!\n");


    printf("\n");
    return 0;
}
