# contact-management-system
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include &lt;string.h&gt;
struct Contact {
char name[50];
char phone[15];
char email[50];
};
void addContact() {
FILE *fp = fopen(&quot;contacts.txt&quot;, &quot;a&quot;);
struct Contact c;
printf(&quot;Enter Name: &quot;);
scanf(&quot;%s&quot;, c.name);
printf(&quot;Enter Phone: &quot;);
scanf(&quot;%s&quot;, c.phone);
printf(&quot;Enter Email: &quot;);

scanf(&quot;%s&quot;, c.email);
fwrite(&amp;c, sizeof(c), 1, fp);
fclose(fp);
printf(&quot;Contact Added Successfully!\n&quot;);
}
void viewContacts() {
FILE *fp = fopen(&quot;contacts.txt&quot;, &quot;r&quot;);
struct Contact c;
printf(&quot;\n--- Contact List ---\n&quot;);
while(fread(&amp;c, sizeof(c), 1, fp)) {
printf(&quot;Name: %s\nPhone: %s\nEmail: %s\n\n&quot;,
c.name, c.phone, c.email);
}
fclose(fp);
}
void searchContact() {
FILE *fp = fopen(&quot;contacts.txt&quot;, &quot;r&quot;);
struct Contact c;
char searchName[50];
int found = 0;
printf(&quot;Enter Name to Search: &quot;);
scanf(&quot;%s&quot;, searchName);
while(fread(&amp;c, sizeof(c), 1, fp)) {
if(strcmp(c.name, searchName) == 0) {
printf(&quot;Contact Found!\n&quot;);
printf(&quot;Name: %s\nPhone: %s\nEmail: %s\n&quot;,
c.name, c.phone, c.email);
found = 1;
}
}
if(!found)
printf(&quot;Contact Not Found!\n&quot;);
fclose(fp);
}
void deleteContact() {
FILE *fp = fopen(&quot;contacts.txt&quot;, &quot;r&quot;);
FILE *temp = fopen(&quot;temp.txt&quot;, &quot;w&quot;);
struct Contact c;
char deleteName[50];
int found = 0;
printf(&quot;Enter Name to Delete: &quot;);
scanf(&quot;%s&quot;, deleteName);
while(fread(&amp;c, sizeof(c), 1, fp)) {
if(strcmp(c.name, deleteName) != 0) {
fwrite(&amp;c, sizeof(c), 1, temp);
} else {
found = 1;
}
}

fclose(fp);
fclose(temp);
remove(&quot;contacts.txt&quot;);
rename(&quot;temp.txt&quot;, &quot;contacts.txt&quot;);
if(found)
printf(&quot;Contact Deleted Successfully!\n&quot;);
else
printf(&quot;Contact Not Found!\n&quot;);
}
int main() {
int choice;
do {
printf(&quot;\n--- Contact Management System ---\n&quot;);
printf(&quot;1. Add Contact\n&quot;);
printf(&quot;2. View Contacts\n&quot;);
printf(&quot;3. Search Contact\n&quot;);
printf(&quot;4. Delete Contact\n&quot;);
printf(&quot;5. Exit\n&quot;);
printf(&quot;Enter your choice: &quot;);
scanf(&quot;%d&quot;, &amp;choice);
switch(choice) {
case 1: addContact(); break;
case 2: viewContacts(); break;
case 3: searchContact(); break;
case 4: deleteContact(); break;
case 5: printf(&quot;Exiting Program...\n&quot;); break;
default: printf(&quot;Invalid Choice!\n&quot;);
}
} while(choice != 5);
return 0;
}
