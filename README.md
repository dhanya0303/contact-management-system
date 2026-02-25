#include <stdio.h>
#include <stdlib.h>
#include <string.h> 
struct Contact { 
char name[50]; 
char phone[15]; 
char email[50]; 
}; 
void addContact() { 
FILE *fp = fopen("contacts.txt", "a"); 
struct Contact c; 
printf("Enter Name: "); 
scanf("%s", c.name); 
printf("Enter Phone: "); 
scanf("%s", c.phone); 
printf("Enter Email: ");

scanf("%s", c.email); 
fwrite(&c, sizeof(c), 1, fp); 
fclose(fp); 
printf("Contact Added Successfully!\n"); 
} 
void viewContacts() { 
FILE *fp = fopen("contacts.txt", "r"); 
struct Contact c; 
printf("\n--- Contact List ---\n"); 
while(fread(&c, sizeof(c), 1, fp))
{ 
printf("Name: %s\nPhone: %s\nEmail: %s\n\n", c.name, c.phone, c.email); 
} 
fclose(fp); 
} 
void searchContact() {
FILE *fp = fopen("contacts.txt", "r");
struct Contact c;
char searchName[50]; 
int found = 0; 
printf("Enter Name to Search: "); 
scanf("%s", searchName); 
while(fread(&c, sizeof(c), 1, fp)) 
{
if(strcmp(c.name, searchName) == 0) 
{ 
printf("Contact Found!\n"); 
printf("Name: %s\nPhone: %s\nEmail: %s\n", c.name, c.phone, c.email); 
found = 1;
} 
} 
if(!found) 
printf("Contact Not Found!\n");
fclose(fp); 
}
void deleteContact() {
FILE *fp = fopen("contacts.txt", "r"); 
FILE *temp = fopen("temp.txt", "w"); 
struct Contact c; 
char deleteName[50]; 
int found = 0; 
printf("Enter Name to Delete: ");
scanf("%s", deleteName); 
while(fread(&c, sizeof(c), 1, fp)) 
{
if(strcmp(c.name, deleteName) != 0) {
fwrite(&c, sizeof(c), 1, temp);
}
else
{
found = 1;
}
}

fclose(fp); 
fclose(temp); 
remove("contacts.txt");
rename("temp.txt", "contacts.txt"); 
if(found) 
printf("Contact Deleted Successfully!\n");
else{
printf("Contact Not Found!\n");
} 
int main() {
int choice; 
do 
{ 
printf("\n--- Contact Management System ---\n"); 
printf("1. Add Contact\n");
printf("2. View Contacts\n"); 
printf("3. Search Contact\n");
printf("4. Delete Contact\n"); 
printf("5. Exit\n");
printf("Enter your choice: "); 
scanf("%d", &choice); 
switch(choice) 
{
case 1: 
addContact();
break;
case 2:
viewContacts(); 
break; 
case 3:
searchContact();
break;
case 4: 
deleteContact(); 
break;
case 5:
printf("Exiting Program...\n");
break;
default: 
printf("Invalid Choice!\n");
}
}
while(choice != 5);
return 0; 
}
