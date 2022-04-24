//Project Title:Bank Management System
#include<stdio.h>
#include<conio.h>
#include<string.h>
#include<process.h>

struct Employee{
  char name[51],email[51],mobile[11],branch[51];
};

struct Customer{
  char name[51],email[51],mobile[11],branch[51],aadhar[50],account[50];
};
//login screen
void screen1();

//Main menu
void screen11();

//Sub menu for Employee management
void screen111();

///Data Entry for adding an Employee
void screen1111();

//view employee
void screen1112();

//search employee
void screen1113();

//update employee
void screen1114();

//Sub menu for Customer management
void screen112();

//Data Entry for adding a customer
void screen1121();

//view customer
void screen1122();

//search customer
void screen1123();

//update customer
void screen1124();

// Function to center the string in given row and color
void center(char *str,int row,int color);

//Function to create color box with White color
void colorbox(int size);

// Function to display message at the bottom of console screen
void message(char *message);

void main(){
  screen1();
  }
void screen1(){
  char userid[51],password[51],ch;
  int i=0;
  clrscr();
  center("Bank Management System",5,YELLOW);
  gotoxy(20,10);printf("User ID");
  gotoxy(20,12);printf("Password");
  gotoxy(35,10);colorbox(30);
  gotoxy(35,12);colorbox(30);
  gotoxy(35,10);gets(userid);
  gotoxy(35,12);
  fflush(stdin);
  while(i<50){
       ch=getch();
       if(ch==13){ //Enter key
    break;
       }
       if(ch==8){ //Backspace
    int n;
    if(i>0)
    { i--;
      gotoxy(35,12);clreol(); //clear till end of line
      gotoxy(35,12); for(n=0;n<i;n++) putchar('*');
    }
       }
       else{
    password[i]=ch;
    putchar('*');
    i++;
       }
  }
  password[i]='\0';
  if(strcmp(userid,"admin")==0  && strcmp(password,"123456")==0)
  {

    gotoxy(20,24);colorbox(50);
    message("Success---You are about to login");
    printf("\n");
    system("pause");
    screen11();
  }
  else{
    gotoxy(20,24);colorbox(40);
    message("Invalid user id or password");
    getch();
  }
}
void screen11(){
  char choice;
  clrscr();
  center("Main Menu:Bank Management System",5,YELLOW);
  center("Employee Management",8,5);
  center("Customer Management",10,5);
  center("Quit Application",12,5);
  gotoxy(1,24);colorbox(79);
  message("Enter choice E->Employee,A->Agent,C->Customer,Q->QuitApp");
  gotoxy(20,20);printf("Enter choice:");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'e': screen111();break;
    case 'c': screen112();break;
    case 'q': exit(0);
  }
}
void screen111(){
  char choice;
  clrscr();
  center("Sub Menu - Employee Management",5,YELLOW);
  center("Add new Employee",8,5);
  center("View all Employee",10,5);
  center("Search an Employee",12,5);
  center("Update Record of an Employee",14,5);
  center("Return to Main menu",16,5);
  gotoxy(20,24);colorbox(60);
  message("                   Enter: A->Add,V->View,S->Search,U->Update,R->Return"   );
  gotoxy(20,20);printf("Enter choice:");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'a': screen1111();break;
    case  'v': screen1112();break;
     case 's': screen1113();break;
     case 'u': screen1114();break;
    case  'r': screen11();break;// returns to main menu
  }
}
void screen1111(){
  struct Employee e;
  char choice=0;
  for(;;){
    if(choice==0)
  clrscr();
  center("Add new Employee",5,YELLOW);
  gotoxy(20,8);
  printf("Employee Name");
  gotoxy(20,10);
  printf("Email");
  gotoxy(20,12);
  printf("Mobile");
  gotoxy(20,14);
  printf("Branch");
  if(choice==0){
  gotoxy(35,8);colorbox(30);
  gotoxy(35,10);colorbox(30);
  gotoxy(35,12);colorbox(10);
  gotoxy(35,14);colorbox(30);
      }
    if(choice!='s'&& choice!='y'&& choice!='n'){
  gotoxy(20,24);colorbox(40);
  message("Enter full name of Employee");
  gotoxy(35,8);fflush(stdin);gets(e.name);

  gotoxy(20,24);colorbox(40);
  message("Enter valid Email of Employee");
  gotoxy(35,10);scanf("%s",e.email);

  gotoxy(20,24);colorbox(40);
  message("Enter 10 digit Mobile Number");
  gotoxy(35,12);scanf("%s%*c",e.mobile);

  gotoxy(20,24);colorbox(40);
  message("Enter Branch of Employee");
  gotoxy(35,14);fflush(stdin);gets(e.branch);
  }
  gotoxy(20,24);colorbox(40);
  message("Enter choice S->Save,E->Edit,R->Return");
  gotoxy(20,18);printf("Enter choice:");
  fflush(stdin);
  scanf("%c%*c",&choice);
  switch(choice){
    case 's':case 'S':
    //code to save data of an employee
    gotoxy(20,20);
    printf("Save record [Y/N] ? ");
    choice=tolower(getchar());
    if(choice=='y')
    {
    FILE *fp=fopen("employee.bin","rb+");
    if(fp==NULL)
    fp=fopen("employee.bin","wb+");
    fseek(fp,0,SEEK_END); //bottom of the file
    fwrite(&e,sizeof(e),1,fp);
    fclose(fp);
    gotoxy(20,24);colorbox(40);
    message("Record Saved... Press any key to continue");
    fflush(stdin);
    }
    break;
    case 'e':case 'E':
    break;
    case 'r': screen111();break;// returns to employee sub menu
    
  }
    }
}
void screen1112(){
   struct Employee e;
     int sno=1,j;
    char choice;
    FILE *fp;
   clrscr();
   center("Employee List",2,YELLOW);
    gotoxy(5,5);
 printf("%-15s %-15s %-15s %-15s %-15s","S.No","Name","Email","Mobile","Branch");
    gotoxy(5,6);
    printf("------------------------------------------------------------------------");
    fp=fopen("employee.bin","rb+");
    if(fp == NULL){
  gotoxy(10,8);
  printf("Error opening file.");
  exit(1);
    }
    j=8;
    while(fread(&e,sizeof(e),1,fp) == 1){
  gotoxy(5,j);
      printf("%-15d %-15s %-15s %-15s %-15s",sno,e.name,e.email,e.mobile,e.branch);
       sno++;
        j++;
    }
  fclose(fp);
  gotoxy(20,24);colorbox(40);
  message("Enter R >Return to Employee Sub menu");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'r': screen111();break;
      
  }
}
void screen1113(){
struct Employee e;
    char choice;
    char email[20];
    FILE *fp;
    clrscr();
    center ("Searching details of an employee",5,YELLOW);
    gotoxy(7,8);
    printf("Enter email of employee whose record you want to search : ");
    fflush(stdin);
    gets(email);
    fp=fopen("employee.bin","rb+");
    if(fp == NULL){
            printf("Error opening file");
        exit(1);
    }
    while(fread(&e,sizeof(e),1,fp ) == 1){
        if(strcmp(email,e.email) == 0){
            gotoxy(20,10);
            printf("Name");
            gotoxy(20,12); 
             printf("email");
            gotoxy(20,14);
            printf("Mobile");
            gotoxy(20,16);
            printf("Branch");

            gotoxy(35,10);colorbox(30);
            gotoxy(35,12);colorbox(30);
            gotoxy(35,14);colorbox(30);
            gotoxy(35,16);colorbox(30);

      gotoxy(35,10);fflush(stdin);printf("%s",e.name);
      gotoxy(35,12);fflush(stdin);printf("%s",e.email);
      gotoxy(35,14);fflush(stdin);printf("%s",e.mobile);
      gotoxy(35,16);fflush(stdin);printf("%s",e.branch);
        }
    }
    fclose(fp);
    gotoxy(20,24);colorbox(40);
  message("Enter R >Return to Employee Sub menu");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'r': screen111();break;
      
  
}
}
void screen1114()
{
    struct Employee e;
    char choice;
    char email[20];
    FILE *fp;
    clrscr();
    center ("Updating details of an employee",5,YELLOW);
    gotoxy(7,7);
    printf("Enter email of employee whose record you want to update : ");
    fflush(stdin);
    gets(email);
    fp=fopen("employee.bin","rb+");
    if(fp == NULL){
            printf("Error opening file");
        exit(1);
    }
    rewind(fp);
   fflush(stdin);
    while(fread(&e,sizeof(e),1,fp) == 1)
    {
        if(strcmp(email,e.email) == 0){
  gotoxy(20,9);
  printf("Employee Name");
  gotoxy(20,11);
  printf("Email");
  gotoxy(20,13);
  printf("Mobile");
  gotoxy(20,15);
  printf("Branch");

  gotoxy(35,9);colorbox(30);
  gotoxy(35,11);colorbox(30);
  gotoxy(35,13);colorbox(10);
  gotoxy(35,15);colorbox(30);

  gotoxy(20,24);colorbox(40);
  message("Enter full name of Employee");
  gotoxy(35,9);fflush(stdin);gets(e.name);

  gotoxy(20,24);colorbox(40);
  message("Enter valid Email of Employee");
  gotoxy(35,11);scanf("%s",e.email);

  gotoxy(20,24);colorbox(40);
  message("Enter 10 digit Mobile Number");
  gotoxy(35,13);scanf("%s%*c",e.mobile);

  gotoxy(20,24);colorbox(40);
  message("Enter Branch of Employee");
  gotoxy(35,15);fflush(stdin);gets(e.branch);
            fseek(fp ,-sizeof(e),SEEK_CUR);
            fwrite(&e,sizeof(e),1,fp);
            break;
        }
    }
    fclose(fp);
    gotoxy(20,24);colorbox(40);
  message("Enter R >Return to Employee Sub menu");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'r': screen111();break;
      
   }
}
void screen112(){
  char choice;
  clrscr();
  center("Sub Menu - Customer Management",5,YELLOW);
  center("Add new Customer",8,5);
  center("View all Customer",10,5);
  center("Search an Customer",12,5);
  center("Update Record of an Customer",14,5);
  center("Return to Main menu",16,5);
  gotoxy(20,24);colorbox(60);
  message("                   Enter: A->Add,V->View,S->Search,U->Update,R->Return"   );
  gotoxy(20,20);printf("Enter choice:");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'a': screen1121();break;
    case 'v': screen1122();break;
    case 's': screen1123();break;
    case 'u': screen1124();break;
    case 'r': screen11();break;
}}
void screen1121(){
  struct Customer c;
  char choice=0;
  for(;;){
    if(choice==0)
  clrscr();
  center("Add new Customer",5,YELLOW);
  gotoxy(20,8);
  printf("Customer Name");
  gotoxy(20,10);
  printf("Email");
  gotoxy(20,12);
  printf("Mobile");
  gotoxy(20,14);
  printf("Branch");
  gotoxy(20,16);
  printf("Aadhar No");
  gotoxy(20,18);
  printf("Account No");
  if(choice==0){
  gotoxy(45,8);colorbox(30);
  gotoxy(45,10);colorbox(30);
  gotoxy(45,12);colorbox(30);
  gotoxy(45,14);colorbox(30);
    gotoxy(45,16);colorbox(30);
   gotoxy(45,18);colorbox(30);
      }
    if(choice!='s'&& choice!='y'&& choice!='n'){
  gotoxy(20,24);colorbox(40);
  message("Enter full name ");
  gotoxy(45,8);fflush(stdin);gets(c.name);

  gotoxy(20,24);colorbox(40);
  message("Enter valid Email ");
  gotoxy(45,10);scanf("%s",c.email);

  gotoxy(20,24);colorbox(40);
  message("Enter 10 digit Mobile Number");
  gotoxy(45,12);scanf("%s%*c",c.mobile);

  gotoxy(20,24);colorbox(40);
  message("Enter Branch ");
  gotoxy(45,14);fflush(stdin);gets(c.branch);

  gotoxy(20,24);colorbox(40);
  message("Enter Aadhar no. ");
  gotoxy(45,16);fflush(stdin);scanf("%s%*c",c.aadhar);

  gotoxy(20,24);colorbox(40);
  message("Enter Account no. ");
  gotoxy(45,18);fflush(stdin);scanf("%s%*c",c.account);
  }
  gotoxy(20,24);colorbox(40);
  message("Enter choice S->Save,E->Edit,R->Return");
  gotoxy(20,20);printf("Enter choice:");
  fflush(stdin);
  scanf("%c%*c",&choice);
  switch(choice){
    case 's':case 'S':
    //code to save data of an employee
    gotoxy(20,22);
    printf("Save record [Y/N] ? ");
    choice=tolower(getchar());
    if(choice=='y')
    {
    FILE *fp=fopen("customer.bin","rb+");
    if(fp==NULL)
    fp=fopen("customer.bin","wb+");
    fseek(fp,0,SEEK_END); //bottom of the file
    fwrite(&c,sizeof(c),1,fp);
    fclose(fp);
    gotoxy(20,24);colorbox(40);
    message("Record Saved... Press any key to continue");
    fflush(stdin);
    }
    break;
    case 'e':case 'E':
    break;
    case 'r': screen112();break;// returns to employee sub menu
    
  }
  }
}
void screen1122(){
   struct Customer c;
     int sno=1,j;
    char choice;
    FILE *fp;
   clrscr();
   center("Customer List",2,YELLOW);
    gotoxy(2,5);
    printf("%-8s %-15s %-15s %-10s %-10s %-8s %-8s","S.No","Name","Email","Mobile","Branch","Aadhar","Account");
     gotoxy(2,6);
    printf("-------------------------------------------------------------------------------");
    fp=fopen("customer.bin","rb+");
    if(fp == NULL){
  gotoxy(10,8);
  printf("Error opening file.");
  exit(1);
    }
    j=8;
    while(fread(&c,sizeof(c),1,fp) == 1){
  gotoxy(2,j);
      printf("%-8d %-15s %-15s %-10s %-10s %-8s %-8s",sno,c.name,c.email,c.mobile,c.branch,c.aadhar,c.account);
       sno++;
        j++;
    }
  fclose(fp);
  gotoxy(20,24);colorbox(40);
  message("Enter R >Return to Customer Sub menu");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'r': screen112();break;
      
  }
}
void screen1123(){
struct Customer c;
    char choice;
    char email[20];
    FILE *fp;
    clrscr();
    center ("Searching details of a Customer",5,YELLOW);
    gotoxy(7,8);
    printf("Enter email of customer whose record you want to search : ");
    fflush(stdin);
    gets(email);
    fp=fopen("customer.bin","rb+");
    if(fp == NULL){
      printf("Error opening file");
  exit(1);
    }
    while(fread(&c,sizeof(c),1,fp ) == 1){
        if(strcmp(email,c.email) == 0){
            gotoxy(20,10);
            printf("Name");
            gotoxy(20,12); 
             printf("email");
            gotoxy(20,14);
            printf("Mobile");
            gotoxy(20,16);
            printf("Branch");
            gotoxy(20,18);
            printf("Aadhar No");
            gotoxy(20,20);
            printf("Account No");

            gotoxy(35,10);colorbox(30);
            gotoxy(35,12);colorbox(30);
            gotoxy(35,14);colorbox(30);
            gotoxy(35,16);colorbox(30);
            gotoxy(35,18);colorbox(30);
            gotoxy(35,20);colorbox(30);

      gotoxy(35,10);fflush(stdin);printf("%s",c.name);
      gotoxy(35,12);fflush(stdin);printf("%s",c.email);
      gotoxy(35,14);fflush(stdin);printf("%s",c.mobile);
      gotoxy(35,16);fflush(stdin);printf("%s",c.branch);
      gotoxy(35,18);fflush(stdin);printf("%s",c.aadhar);
      gotoxy(35,20);fflush(stdin);printf("%s",c.account);
     
        }
    }
    fclose(fp);
    gotoxy(20,24);colorbox(40);
  message("Enter R >Return to Customer Sub menu");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'r': screen112();break;
      
  
}
}
void screen1124()
{
    struct Customer c;
    char choice;
    char email[20];
    FILE *fp;
    clrscr();
    center ("Updating details of a Customer",5,YELLOW);
    gotoxy(7,8);
    printf("Enter email of customer whose record you want to update : ");
    fflush(stdin);
    gets(email);
    fp=fopen("customer.bin","rb+");
    if(fp == NULL){
            printf("Error opening file");
        exit(1);
    }
    rewind(fp);
   fflush(stdin);
    while(fread(&c,sizeof(c),1,fp) == 1)
    {
        if(strcmp(email,c.email) == 0){
  gotoxy(20,10);
  printf("Customer Name");
  gotoxy(20,12);
  printf("Email");
  gotoxy(20,14);
  printf("Mobile");
  gotoxy(20,16);
  printf("Branch");
  gotoxy(20,18);
  printf("Aadhar No");
  gotoxy(20,20);
  printf("Account No");

  gotoxy(35,10);colorbox(30);
  gotoxy(35,12);colorbox(30);
  gotoxy(35,14);colorbox(30);
  gotoxy(35,16);colorbox(30);
  gotoxy(35,18);colorbox(30);
  gotoxy(35,20);colorbox(30);

  gotoxy(20,24);colorbox(40);
  message("Enter full name of Customer");
  gotoxy(35,10);fflush(stdin);gets(c.name);

  gotoxy(20,24);colorbox(40);
  message("Enter valid Email");
  gotoxy(35,12);scanf("%s",c.email);

  gotoxy(20,24);colorbox(40);
  message("Enter 10 digit Mobile Number");
  gotoxy(35,14);scanf("%s%*c",c.mobile);

  gotoxy(20,24);colorbox(40);
  message("Enter Branch of Employee");
  gotoxy(35,16);fflush(stdin);gets(c.branch);

  gotoxy(20,24);colorbox(40);
  message("Enter Aadhar No");
  gotoxy(35,18);fflush(stdin);scanf("%s%*c",c.aadhar);

  gotoxy(20,24);colorbox(40);
  message("Enter Account No");
  gotoxy(35,20);fflush(stdin);scanf("%s%*c",c.account);

      fseek(fp ,-sizeof(c),SEEK_CUR);
      fwrite(&c,sizeof(c),1,fp);
            break;
        }
    }
      fclose(fp);
    gotoxy(20,24);colorbox(40);
  message("Enter R >Return to Customer Sub menu");
  fflush(stdin);
  choice=tolower(getchar());
  switch(choice){
    case 'r': screen112();break;
      
   }
}
void center(char *str,int row,int color){
  int col=40-strlen(str)/2;
  gotoxy(col,row);
  textcolor(color);
  cprintf(str);
  textcolor(WHITE);
}
void message(char *message){
  int col=40-strlen(message)/2;
  gotoxy(col,24);
  printf(message);
}
void colorbox(int size){
  int i;
  textbackground(BLUE);
  for(i=1;i<size;i++)
  cprintf(" ");
  textbackground(BLACK);
}
