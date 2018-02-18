#include<stdio.h>
#include<conio.h>
#include<string.h>
#include<process.h>
#include<stdlib.h>
#include<dos.h>
struct placement {
     int stud;
     int comp[100];
}p;

struct company {
             int cId;
             char cname[50];
             char job[30];
            long int salary;
}c;
struct student {
        int sId;
        char name[30];
        long int ph;
        char course[30];
        char add[50];
        char email[30];
        float cgpa;
    }s;

    char a,query[30],name[30];
    FILE *fp, *ft,*f,*f1;
int i,n,choice,l,found;
void studentDetails(){
     top:
    system("cls");
    printf( "\t\t====== STUDENT INFORMATION SYSTEM ======");
    printf("\n\n                                          ");
    printf("\n\n");
    printf("\n \t\t\t 0: back ");
    printf("\n \t\t\t 1. Add student Detail");
    printf("\n \t\t\t 2. display list   ");
    printf("\n \t\t\t 3: search student detail");
    printf("\n \t\t\t 4. Modify student detail");
    printf("\n \t\t\t 5. Delete student detail");
    printf( "\n\n");
     printf( "\t\t\t Select Your Choice :=> ");
     scanf("%d",&choice);
     switch(choice)
     {
     case 1:
        system("cls");
        fp=fopen("student.dll","a");
        for (;;)
        { fflush(stdin);
        printf("enter the full name:");
        scanf("%[^\n]",&s.name);
        fflush(stdin);
        printf("id number:");
        scanf("%d",&s.sId);
        fflush(stdin);
        printf("course:");
        scanf("%s",&s.course);
        fflush(stdin);
        printf("cgpa:");
        scanf("%f",&s.cgpa);
        fflush(stdin);
        printf("Phone:");
        scanf("%ld",&s.ph);
        fflush(stdin);
        printf("address:");
        scanf("%[^\n]",&s.add);
        fflush(stdin);
        printf("email address:");
        gets(s.email);
        printf("\n");

        fwrite(&s,sizeof(s),1,fp);
        printf("\n Add Another Record (Y/N) ");
          a=getch();
          if(a=='n'||a=='Y')
            break;
           }
        fclose(fp);
        goto top;
     case 2:
        system("cls");
        printf("\n\t\t================================\n\t\t\tLIST OF STUDENT\n\t\t================================\n\n\n");
        fp=fopen("student.dll","r");
        fflush(stdin);
        found=0;
        while(fread(&s,sizeof(s),1,fp)==1){
        printf("\nid\t: %d\nName\t: %s\ncourse\t: %s\ncgpa\t: %f\nPhone\t: %ld\nAddress\t: %s\nEmail\t: %s\n",s.sId,s.name,s.course,s.cgpa,s.ph,s.add,s.email);
        found++;
        getch();
       }
        fclose(fp);
        if(found==0)
            printf("\n\n\t\t LIST IS EMPTY");
        printf("=========================================================== \n\n");
//
       goto top;
     case 3:
        system("cls");
        do
        {
        found=0;
        printf("\n\n\t..::student SEARCH\n\t===========================\n\t..::Name  to search: ");
        fflush(stdin);
        scanf("%[^\n]",&query);
        l=strlen(query);
        fp=fopen("student.dll","r");

        system("cls");
        printf("\n\n..::Search result for '%s' \n===================================================\n",query);
        while(fread(&s,sizeof(s),1,fp)==1)
        {
        for(i=0;i<=l;i++)
        name[i]=s.name[i];
        name[l]='\0';
        if(stricmp(name,query)==0)
        {
        printf("\nName\t: %s\ncourse\t: %s\ncgpa\t: %f\nPhone\t: %ld\nAddress\t: %s\nEmail\t: %s\n",s.name,s.course,s.cgpa,s.ph,s.add,s.email);
        found++;
        if (found%4==0)
        {
        printf("..::Press any key to continue...");
        getch();
        }
        }
        }

        if(found==0)
        printf("\n..::No match found!");
        else
        printf("\n..::%d match(s) found!",found);
        fclose(fp);
        printf("\n ..::Try again?[y/n]\n\t");
        a=getch();
        if(a=='n'||a=='N')
          break;
        }while(1);
        goto top;


     case 4:
                 system("cls");
        fp=fopen("student.dll","r");
        ft=fopen("temp.dat","w");
        fflush(stdin);
        printf("..::Edit detail\n===============================\n\n\t..::Enter the name to edit:");
        scanf("%[^\n]",name);
        while(fread(&s,sizeof(s),1,fp)==1)
        {
        if(stricmp(name,s.name)!=0)
        fwrite(&s,sizeof(s),1,ft);
        }
        fflush(stdin);
        printf("\n\n..::Editing '%s'\n\n",name);
        printf("..::Name(Use identical):");
        scanf("%[^\n]",&s.name);
        fflush(stdin);
        printf("..::course:");
        scanf("%[^\n]",&s.course);
        fflush(stdin);
        printf("..::cgpa:");
        scanf("%f",&s.cgpa);
        fflush(stdin);
        printf("..::Phone:");
        scanf("%ld",&s.ph);
        fflush(stdin);
        printf("..::address:");
        scanf("%[^\n]",&s.add);
        fflush(stdin);
        printf("..::email address:");
        gets(s.email);
        printf("\n");
        fwrite(&s,sizeof(s),1,ft);
        fclose(fp);
        fclose(ft);
        remove("student.dll");
        rename("temp.dat","student.dll");
        goto top;

     case 5:
                     system("cls");
            fflush(stdin);
            printf("\n\n\t..::DELETE A STUDENT DETAIL\n\t==========================\n\t..::Enter the name of student to delete:");
            scanf("%[^\n]",&name);
            fp=fopen("student.dll","r");
            ft=fopen("temp.dat","w");
            while(fread(&s,sizeof(s),1,fp)!=0)
            if (stricmp(name,s.name)!=0)
            fwrite(&s,sizeof(s),1,ft);
            fclose(fp);
            fclose(ft);
            remove("student.dll");
            rename("temp.dat","student.dll");
            goto top;

     case 0:
            break;
    default:
            printf("Invalid choice");
            goto top;



     }

}
void companyDetail()
{   top1:
    system("cls");
     printf( "\t\t====== COMPANY INFORMATION SYSTEM ======");
    printf("\n\n                                          ");
    printf("\n\n");
    printf("\n \t\t\t 1. Add    companyDetails");
    printf("\n \t\t\t 2. display companylist  ");
    printf("\n \t\t\t 3. Delete companydetail");
     printf("\n \t\t\t 0. back");
     printf( "\n\n");
     printf( "\t\t\t Select Your Choice :=> ");
     scanf("%d",&choice);
     switch(choice)
     {
     case 1:

        system("cls");
        fp=fopen("company.dll","a");
        for (;;)
        { fflush(stdin);
        printf("enter the company name:");
        scanf("%[^\n]",&c.cname);
        fflush(stdin);
        printf("register number:");
        scanf("%d",&c.cId);
        fflush(stdin);
        printf("job:");
        scanf("%s",&c.job);
        fflush(stdin);
        printf("salary package:");
        scanf("%ld",&c.salary);
        fflush(stdin);
        printf("\n");
        fwrite(&c,sizeof(c),1,fp);
        printf("\n Add Another Record (Y/N) ");
         a=getchar();
         if(a=='n'||a=='N')
            break;
           }
        fclose(fp);
        goto top1;
     case 2:
         system("cls");
        printf("\n\t\t================================\n\t\t\tLIST OF company\n\t\t================================\n\n\n");
        fp=fopen("company.dll","r");
        fflush(stdin);
        found=0;
        while(fread(&c,sizeof(c),1,fp)==1)
        {
        printf("\n\n\tregister number\t: %d\n\tName\t: %s\n\tjob\t: %s\n\tsalary\t: %ld\n",c.cId,c.cname,c.job,c.salary);
         found++;
        getch();
        }
        fclose(fp);
        if(found==0)
        { printf("\n\n\t LIST IS EMPTY");
       }
        printf("\n\n=========================================================== \n\n");
        getch();
       goto top1;
     case 3:
         system("cls");
            fflush(stdin);
            printf("\n\n\t..::DELETE A COMPANY DETAIL\n\t==========================\n\t..::Enter the name of company to delete:");
            scanf("%[^\n]",&name);
            fp=fopen("company.dll","r");
            ft=fopen("temp.dat","w");
            while(fread(&c,sizeof(c),1,fp)!=0)
            if (stricmp(name,c.cname)!=0)
            fwrite(&c,sizeof(c),1,ft);
            fclose(fp);
            fclose(ft);
            remove("company.dll");
            rename("temp.dat","company.dll");
            goto top1;
     case 4:
        break;

     }

}
void placementdetails()
{
    top2:
   system("cls");
   printf( "\t\t====== PLACEMENT INFORMATION SYSTEM ======");
    printf("\n\n                                          ");
    printf("\n\n");
    printf("\n \t\t\t 1. Add details");
    printf("\n \t\t\t 2. view detail ");
    printf("\n \t\t\t 3.company details");
    printf("\n \t\t\t 4. modify detail");
    printf("\n \t\t\t 5. Delete detail");
     printf("\n \t\t\t 0.back");
     printf( "\n\n");
     printf( "\t\t\t Select Your Choice :=> ");
     scanf("%d",&choice);
   switch(choice)
   {
   case 1:
       p1:
       system("cls");
       printf("\n\n\t..::ADD THE DETAILS\n\t==========================\n");
       ft=fopen("placement.dll","a");
       fp=fopen("student.dll","r");
       f=fopen("company.dll","r");
       printf("enter student id:");
       scanf("%d",&p.stud);
       fflush(stdin);
       printf("enter student name:");
       scanf("%[^\n]",&name);
       fflush(stdin);
       while(fread(&s,sizeof(s),1,fp)==1)
       {
            if(stricmp(name,s.name)==0)
              if(s.sId==p.stud)
                 {
                     n=1;
                     break;

        }
        }
        if(n!=1)
        {
            printf("\n\n\t\tgiven data is not matched\n retry\n");
            printf("\t\twant to continue[y/n]");
            a=getchar();
            if(a=='y'||a=='Y')
                goto p1;
            goto top2;
        fclose(fp);

        }
        while(fread(&c,sizeof(c),1,f)==1)
        {

            printf("\n%d\t %s",c.cId,c.cname);
        }
        fclose(f);
        a='y';

        for(i=0;a=='y'||a=='Y';i++)
        {
            printf("\n\n\t\tenter company id number:");
            scanf("%d",&p.comp[i]);
            printf("\n\t\t enter Y to add more company:");
            a=getch();

        }
        fwrite(&p,sizeof(p),1,ft);
        printf("\n\n\t\twant to enter more detail [y/n] :");
        a=getch();
        if(a=='y'||a=='Y')
            goto p1;
            fclose(ft);
            goto top2;

   case 2:
       p2:
       system("cls");
        printf("\n\n\t..::DISPLAY THE STUDENT PLACEMENT DETAILS\n\t==========================\n");
       printf("\t\tenter the student id:");
       scanf("%d",&l);
      ft=fopen("placement.dll","r");
       fp=fopen("student.dll","r");
       f=fopen("company.dll","r");
       while(fread(&s,sizeof(s),1,fp)==1)
       {
           if(l==s.sId)
           {
               n=1;
               printf("\n\t%d  %s",s.sId,s.name);
               getch();
               break;
           }
       }
       if(n!=1)
       {
       printf("not found");
       printf("want to try again[y/n]");
       a=getch();
       if(a=='y'||a=='Y')
        goto p2;
        goto top2;
       }
       found=0;
       while(fread(&p,sizeof(p),1,ft)==1)
       {
           if(p.stud==l)
           {
               for(i=0;p.comp[i]!='\0';i++)
               {
                   fseek(f,0,0);
                   while(fread(&c,sizeof(c),1,f)==1){
                        if(c.cId==p.comp[i])
                           printf("\n\t\t%d %s",c.cId,c.cname);
                           found++;

                   }

               }

           }

       }
       if(found==0)
       {
           printf("\n\n\t\tnot yet placed");

       }
       printf("\n\n=========================================================== \n\n");
       getch();
       goto top2;
   case 3:
        system("cls");
        printf("\n\t\t=================\t\tPLACEMENT LIST \t\t===================");
        ft=fopen("placement.dll","r");
       fp=fopen("student.dll","r");
       f=fopen("company.dll","r");
       while(fread(&c,sizeof(c),1,f)==1)
       {
           found=0;
           printf("\n\n\t%d  %s",c.cId,c.cname);
         while(fread(&p,sizeof(p),1,ft)==1)
           {
               for(i=0;p.comp[i]!='\0';i++)
               {
                   if(p.comp[i]==c.cId)
                   {
                     while(fread(&s,sizeof(s),1,fp)==1)
                        {
                       if(p.stud==s.sId){
                       found++;
                       printf("\n\t\t%d  %s",s.sId,s.name);
                       break;
                   }
                   }

               }
           }}
           if(found==0)
           {
               printf("\n\t\tnone");
           }
             printf("\n=========================================================== \n\n");
             getch();
             }
             getch();
             goto top2;


   case 4:
        system("cls");
        f1=fopen("placement.dll","r");
        ft=fopen("temp.dat","w");
        fflush(stdin);
        printf("\nEdit detail\n===============================\n\n\tEnter the id to edit:");
        scanf("%d",&n);
        while(fread(&p,sizeof(p),1,f1)==1)
        {
        if(n!=p.stud)
        fwrite(&p,sizeof(p),1,ft);
        }
        fp=fopen("student.dll","r");
       f=fopen("company.dll","r");
       printf("enter student id:");
       scanf("%d",&p.stud);
       fflush(stdin);
       printf("\n\tenter student name:");
       scanf("%[^\n]",&name);
       fflush(stdin);
       while(fread(&s,sizeof(s),1,fp)==1)
       {
            if(stricmp(name,s.name)==0)
              if(s.sId==p.stud)
                 {
                     n=1;
                     break;
        }
        }
        if(n!=1)
        {
            printf("\n\tgiven data is not matched\n\t retry\n");
            printf("\twant to continue[y/n]");
            a=getchar();
            if(a=='y'||a=='Y')
                goto p1;
            goto top2;
        fclose(fp);

        }
        while(fread(&c,sizeof(c),1,f)==1)
        {

            printf("%d\t %s\n",c.cId,c.cname);
        }
        fclose(f);
        a='y';

        for(i=0;a=='y'||a=='Y';i++)
        {
            printf("enter company id number:\n");
            scanf("%d",&p.comp[i]);
            printf("enter Y to add more company:\n");
            a=getch();
        }
        fwrite(&p,sizeof(p),1,ft);
        fclose(f1);
        fclose(ft);
        remove("placement.dll");
        rename("temp.dat","placement.dll");
        printf("\n\t\tINFO IS SUCCESSSFULLY MODIFIED");
        getch();
        goto top2;

    case 5:
           system("cls");
            fflush(stdin);
            printf("\n\n\t..::DELETE A PLACEMENT DETAIL\n\t==========================\n\t..::Enter the student id to delete:");
            scanf("%d",&n);
            fp=fopen("placement.dll","r");
            ft=fopen("temp.dat","w");
            while(fread(&p,sizeof(p),1,fp)!=0)
            if (n!=p.stud)
            fwrite(&p,sizeof(p),1,ft);
            fclose(fp);
            fclose(ft);
            remove("placement.dll");
            rename("temp.dat","placement.dll");
            printf("\n\n\t\tsuccessfully deleted");
            getch();
            goto top2;
    case 0:
        break;




   }


}

int main()
{
 main:

    system("cls");
     printf( "\t\t======PLACEMENT INFO  ======");
    printf("\n\n                                          ");
    printf("\n\n");
    printf("\n \t\t\t 1. students details");
    printf("\n \t\t\t 2. company details");
     printf("\n \t\t\t 3. placement details");
    printf("\n \t\t\t 0. exit\n");
     printf( "\n\n");
     printf( "\t\t\t Select Your Choice :=> ");
    scanf("%d",&choice);
switch(choice) {
case 0:
    break;
case 1:studentDetails();
     goto main;

case 2: companyDetail();
     goto main;
case 3:
    placementdetails();
    goto main;

}
}
