#include<stdio.h>
#include<stdlib.h>
#include <windows.h>
#include<time.h>

struct node
{
    int data;
    struct node *link;

}gen;
int valid(int a, int b)
{
    if(a>b)
    {
        return 1;

    }
}
void SetColor(int ForgC)
{
     WORD wColor;

     HANDLE hStdOut = GetStdHandle(STD_OUTPUT_HANDLE);
     CONSOLE_SCREEN_BUFFER_INFO csbi;

     if(GetConsoleScreenBufferInfo(hStdOut, &csbi))
     {
          wColor = (csbi.wAttributes & 0xF0) + (ForgC & 0x0F);
          SetConsoleTextAttribute(hStdOut, wColor);
     }
     return;
}
int extract(struct node*h,int d,int s,int amount)
{
    if (amount<h->data || amount==0)
        return 0;
    else
    {
        int i=0;
        struct node *ptr;
        ptr=h;

        while(i<d)
        {
            ptr=ptr->link;
            ++i;
        }
        h=ptr;
        printf("\n%d notes of %d is withdrawn\n",i,h->data);
        return i;
    }
}
struct node *make(int g,int k)
{
    int i=0,d;
    d=g/k;
    i=0;

    struct node *top=NULL,*ptr=NULL;
    while(i<d)
    {
        if(top==NULL)
        {struct node *temp;
            temp=(struct node *)malloc(sizeof(struct node));
            temp->data=k;
            temp->link=NULL;
            top=temp;
            ptr=temp;

        }
        else
        {
            struct node *temp=(struct node *)malloc(sizeof(struct node));
            temp->data=k;
            temp->link=NULL;
            ptr->link=temp;
            ptr=temp;

        }
        i=i+1;
    }
    printf("%d",i);
    return top;
}
int length(struct node *h)
{
    struct node *ptr;
    int i=0;
    ptr=h;

    while(ptr)
    {
        i++;
        ptr=ptr->link;
    }
    return i;
}
struct bal
{
    int  depo;
    int wid;
    int balance;
    struct bal *next1;
}bal2,*head=NULL;

struct create
{
    char n1[50],n2[50],n3[50];
    char s1[50],s2[50],s3[50],aress[50];
    char passbook[80];
    int num;
    int pin;
    int  aad,ifsc;
    int  accno;
    struct bal *bal3;
    struct create *next;
    FILE *fptr;
}stu,*start=NULL,*cur=NULL;

void ent()
{
    SetColor(14);
    static int mn;
    mn=1;
    int i=1;

    printf("WELCOME CUSTOMER PLEASE ENTER YOUR DETAILS FOR THE ACCOUNT GENERATION **\n");

    while(i==1)
    {
        struct create *ptr;
        struct bal *ptr2;
        ptr2=(struct bal*)malloc(sizeof(bal2));
        ptr=(struct create*)malloc(sizeof(stu));

        printf("\nEnter the following entries\n");

        printf("\nEnter the first name of the applicant=\t");
        scanf("%s",ptr->n1);

        printf("\nEnter the second name of the applicant=\t");
        scanf("%s",ptr->s1);

        printf("\nEnter the first name of the father=\t");
        scanf("%s",ptr->n2);

        printf("\nEnter the second name of the father=\t");
        scanf("%s",ptr->s2);

        printf("\nEnter the first name of the mother=\t");
        scanf("%s",ptr->n3);

        printf("\nEnter the second name of the mother=\t");
        scanf("%s",ptr->s3);

        printf("\nEnter your address=\t");
        scanf("%s",ptr->aress);

        printf("\n Enter the number u want to link wid the account=\t");
        scanf("%d",&ptr->num);

        printf("\n Enter the creation amount =\t");

        scanf("%d",&ptr2->balance);
        ptr2->depo=ptr2->balance;
        ptr->bal3=ptr2;

        printf("\n Enter the aadhar number of the applicant-\t");
        scanf("%d",&ptr->aad);
        strcat(ptr->passbook,ptr->n1);
        strcat(ptr->passbook,ptr->aress);
        strcat(ptr->passbook,".txt");

        ptr->accno=mn;
        mn=mn+1;

        printf("\n YOUR ACCOUNT NUMBER IS =\t%d",ptr->accno);
        printf("\n SET THE PIN FOR UR ACCOUNT = \t");
        scanf("%d",&ptr->pin);
        ptr->next=NULL;
        ptr2->next1=NULL;

        if(start==NULL)
        {
            start=ptr;
            cur=ptr;
        }
        else
        {
            cur->next=ptr;
            cur=ptr;
        }

        ptr->fptr=fopen(ptr->passbook,"a+");
        fprintf(ptr->fptr,"balance    deposit      withdraw \n");
        fclose(ptr->fptr);
        ptr->bal3->depo=0;
        ptr->bal3->wid=0;

        time_t t;
        time(&t);
        ptr->fptr=fopen(ptr->passbook,"a+");
        fprintf(ptr->fptr,"%d         %d           %d      Date and Time is%s\n",ptr->bal3->balance,ptr->bal3->depo,ptr->bal3->wid,ctime(&t));
        fclose(ptr->fptr);


        printf("\n\n\n\n\n\n\t\t\t\t\t | | Account is successfully created | |\n\n\n\n\n\n\n");
        printf("Press 1 to create a new account ");
        scanf("%d",&i);

    }
}
void disp()
{
    SetColor(rand());
    cur=start;
    while(cur!=NULL)
    {
        printf("\nAccount number                                 |        %d",cur->accno);
        printf("\nAccount holder name                            |        %s %s",cur->n1,cur->s1);
        printf("\nBalance                                        |        %d",cur->bal3->balance);
        printf("\nPhone Numbert                                  |        %d",cur->num);
        printf("\nRegistered Address                             |        %s",cur->aress);
        printf("\nAadhar number                                  |        %d",cur->aad);
        cur=cur->next;
    }
    SetColor(14);
}
void disp1(int d)
{
    cur=start;

    while(cur!=NULL)
    {
        if(cur->accno==d)
        {printf("\nAccount number                                |        %d",cur->accno);
         printf("\nAccount holder name                            |        %s %s",cur->n1,cur->s1);
         printf("\nBalance                                        |        %d",cur->bal3->balance);
         printf("\nPhone Numbert                                  |        %d",cur->num);
         printf("\nRegistered Address                             |        %s",cur->aress);
         printf("\nAadhar number                                  |        %d",cur->aad);}
    cur=cur->next;
    }
}
struct create *search(int acc)
{
    struct create *t=start;
    while(t)
    {
        if(t->accno==acc){
            return t;
            break;
        }
        t=t->next;
    }
    return NULL;
}
void update()
{
    int n;
    printf("\n\n\n\n\n\nDo you want to update the data present in the database if yes press 1 else press 0");
    scanf("%d",&n);

    if(n==1)
    {
        printf("\n\n\n\n\n\n\t\t\t\tPlease Enter the Account number whose information u want to update\n");
        int acc;
        printf("\n Enter the account number =\t");
        scanf("%d",&acc);

        struct create *ptr;
        ptr=search(acc);

        if(ptr){
            printf("Now Enter what u want to update\n");
            int num,pincode,aad,pin;
            int n;

            char namf[50],naml[50],add[50],fa[50],ma[50];
            printf("\n Press 1 : Account number\n");
            printf("\n Press 2 : Phone number\n");
            printf("\n Press 3 : Pin code\n");
            printf("\n Press 4 : Aadhaar number\n");
            printf("\n Press 5 : Pin for withdrawal\n");
            printf("\n Press 6 : User First name \n");
            printf("\n Press 7 : User Last name \n");
            printf("\n Press 8 : Address\n");
            printf("\n Press 9 : Father name \n");
            printf("\n Press 10: Mother name\n");
            scanf("%d",&n);

            switch(n)
            {
                case 1:
                    printf("\n Enter new account number\n");
                    scanf("%d",&acc);
                    ptr->accno=acc;
                    break;

                case 2:
                    printf("\n Enter new phone no.\n");
                    scanf("%d",&num);
                    ptr->num=num;
                    break;

                case 3:
                    printf("\n Enter new pincode\n");
                    scanf("%d",&pincode);
                    ptr->pin=pincode;
                    break;

                case 4:
                    printf("\n Enter new aadhar number\n");
                    scanf("%d",&aad);
                    ptr->aad=aad;
                    break;

                case 5:
                    printf("\n Enter new pin\n");
                    scanf("%d",&pin);
                    ptr->pin=pin;
                    break;

                case 6:
                    printf("\n Enter account holder First name\n");
                    scanf("%s",ptr->n1);
                    break;

                case 7:
                    printf("\n Enter account holder Last name\n");
                    scanf("%s",ptr->s2);
                    break;

                case 8:
                    printf("\n Enter the new address of account holder \n");
                    scanf("%s",ptr->aress);
                    break;

                case 9:
                    printf("\n Enter account holder father's name\n");
                    scanf("%s",ptr->n2);
                    break;

                case 10:
                    printf("\n Enter account holder mother's name\n");
                    scanf("%s",ptr->n3);
                    break;

                default:
                    printf("Invalid choice \n");
            }
        }
        else
            printf("\n INVALID ACCOUNT NUMBER \n");
    }
    if(n==0)
    {
        printf("\n\t No changes made");
    }
}
struct create *security()
{
    SetColor(12);
    int acc,a;
    struct create *f;

    printf("\nenter the account number\n");
    scanf("%d",&acc);
    f=search(acc);

    if (f==NULL)
    {
        printf("\nenter the account number correctly\n");
        scanf("%d",&acc);
        f=search(acc);

        if(f==NULL)
            exit(0);
    }
    printf("\n please enter the pin \n");
    int i=3;

    while(i>0)
    {
        printf("\n enter the pin correctly in %d chance else program will close \n",i);
        scanf("%d",&a);
        i=i-1;

        if(a==f->pin)
        {
            disp1(f->accno);
            return f;
        }
        else
        {

            if (i==0)
            {
                exit(0);
            }
            printf("\nenter the pin correctly \n ");
        }
        }
    }
void manage()
{
    int aa=0;
    int a=0;
    int r=0;

    struct create *k;
    k=security();
    printf("\nenter 1 for deposit or 2 for withdraw \n");
    scanf("%d",&aa);

    if (aa==1)
    {
        printf("\nEnter the amount you want to deposit=\t");
        scanf("%d",&a);
        k->bal3->depo=a;
        k->bal3->balance=a+k->bal3->balance;
        k->bal3->wid=0;

        printf("\n Now net balance in your account=%d",k->bal3->balance);
        time_t kj;
        time(&kj);

        k->fptr=fopen(k->passbook,"a+");
        fprintf(k->fptr,"%d      %d      %d      Date and Time is%s\n",k->bal3->balance,k->bal3->depo,k->bal3->wid,ctime(&kj));
        fclose(k->fptr);
        k->bal3->depo=0;
    }
    if(aa==2)
    {
        int r;

        printf("\n YOU WANT TO WITHDRAW MONEY ELECTRONICALLY  TO YOUR PAYTM ACCOUNT OR U WANT CASH\n");
        printf("\n If ELECTONICALLY press 1 else press 2");
        printf("\n if you want to do a account to account transaction enter 3\n");
        scanf("%d",&r);

        if (r==1)
        {
            printf("\nEnter the amount you want to withdraw\n");
            scanf("%d",&a);

            if(a>k->bal3->balance)
            {
                printf("\nThe amount which you entered cant be withdrawn\n");
            }
            else
            {
                k->bal3->wid=a;
                k->bal3->balance=k->bal3->balance-a;
                printf("Now net balance in your account is=%d",k->bal3->balance);
                k->bal3->depo=0;

                time_t po;
                time(&po);
                k->fptr=fopen(k->passbook,"a+");
                fprintf(k->fptr,"%d     %d      %d      Date and Time is%s\n",k->bal3->balance,k->bal3->depo,k->bal3->wid,ctime(&po));
                fclose(k->fptr);
                k->bal3->wid=0;

            }

        }
        if(r==2)
        {
            int g=0,h=0,l=0,j=0,u=0;
            int z=0,x=0,b=0,m=0,r=0,o=0,p=0,e=0;

            printf("\nEnter the amount u want to withdraw in the denomination of 2000,500,100,50\n");
            printf("\n Available balance in ur account =\t%d\n",k->bal3->balance);
            g=k->bal3->balance;

            struct node *ptr;
            struct node *fif;
            struct node *two_th;
            struct node *five_h;
            struct node *hund;

            switch(1)
            {
                case 1:
                    two_th=make(g,2000);
                case 2:
                    five_h=make(g,500);
                case 3:
                    hund=make(g,100);
                case 4:
                    fif=make(g,50);
            }

            printf("\nEnter the no of 2000 notes to withdraw\n");
            scanf("%d",&h);

            printf("\nEnter the no of 500 notes to withdraw\n");
            scanf("%d",&l);

            printf("\nEnter the no of 100 notes to withdraw\n");
            scanf("%d",&j);

            printf("\nEnter the no of 50 notes to withdraw\n");
            scanf("%d",&u);

            printf("\nEnter the amount you want to withdraw\n");
            int amount,op;

            op=h*2000+l*500+j*100+u*50;
            scanf("%d",&amount);

            if(amount!=op)
                printf("\nyour amount does not match with the total money you want to withdraw\n");

            if(amount<=k->bal3->balance)
            {
                z=length(two_th);
                x=length(five_h);
                b=length(hund);
                m=length(fif);

                printf("\nNumber of 2000 available =\t%d",z);
                printf("\nNumber of 500 available =\t%d",x);
                printf("\nNumber of 100 available =\t%d",b);
                printf("\nNumber of 50 available =\t%d",m);

                int lk;
                lk=amount;
                if(z>h)
                    {
                        r=extract(two_th,h,z,amount);
                        k->bal3->balance=k->bal3->balance-r*2000;
                         lk =amount-r*2000;}

                if(x>l)
                    {o=extract(five_h,l,x,lk);
                        k->bal3->balance=k->bal3->balance-o*500;
                         lk =lk-r*500;}

                if(b>j)
                    {p=extract(hund,j,b,lk);
                    k->bal3->balance=k->bal3->balance-p*100;
                    lk =lk-r*100;}

                if(m>u)
                    {e=extract(fif,u,m,lk);
                        k->bal3->balance=k->bal3->balance-e*50;
                        lk =lk-r*50;}

                printf("\nCurrent balance in your account is =\t%d\n",k->bal3->balance);
                k->bal3->wid=amount;
                k->bal3->depo=0;

                time_t hg;
                time(&hg);
                k->fptr=fopen(k->passbook,"a+");
                fprintf(k->fptr,"%d      %d      %d     Date and Time%s\n",k->bal3->balance,k->bal3->depo,k->bal3->wid,ctime(&hg));
                fclose(k->fptr);

            }
            else
                printf("\n\t\t\t\tThe amount you entered cant be withdrawn\n");
        }
    }
    if(r==3)
    {
        struct create *d;
        int h;
        printf("\n Enter the account number  of the recipient\n");
        int acc;
        scanf("%d",&acc);

        d=search(acc);
        printf("\nEnter the amount to transfer\n");
        scanf("%d",&h);
        k->bal3->balance=k->bal3->balance-h;
        k->bal3->wid=h;
        k->bal3->depo=0;

        printf("\n your amount has been withdrawn \n");
        time_t rr;
        time(&rr);
        k->fptr=fopen(k->passbook,"a+");
        fprintf(k->fptr,"%d     %d     %d     Date and Time%s\n",k->bal3->balance,k->bal3->depo,k->bal3->wid,ctime(&rr));
        fclose(k->fptr);

        d->bal3->balance=d->bal3->balance+h;
        d->bal3->wid=0;
        d->bal3->depo=h;

        printf("\n the  amount has been deposited \n");
        time_t vb;
        time(&vb);
        d->fptr=fopen(d->passbook,"a+");
        fprintf(d->fptr,"%d     %d     %d     Date and Time%s\n",d->bal3->balance,d->bal3->depo,d->bal3->wid,ctime(&vb));
        fclose(d->fptr);

    }
}
int main()
{
    SetColor(2);
    printf("                      WELCOME TO ADNP BANK                      \n");
    printf("-----------------------------------------------------------------\n");
    printf("-----------------------------------------------------------------\n");
    printf("   Do you want to enter into the bank if yes press 1 else press 0 \n");

    int z;
    scanf("%d",&z);

    if(z==0){
        printf("***  Process terminated  **** \n\n\n\n");
        exit(0);
    }
    else
        {
    int i=1,n=1,m,k;
    int j;
    printf("\ndo you want to make a account then enter 1\n");
    scanf("%d",&k);

    if(k==1)
        ent();
    printf("\n if you want to update then enter 1\n");
    scanf("%d",&j);

    if(j==1)
        {update();
        printf("\nDo you want to make more changes\n");

    while(i==1)
    {
        printf("\n\t1.)Yes");
        printf("\n\t2.)No");
        scanf("\n%d\n",&i);

        if(i==1)
        {
            update();
        }
    }
        }

    printf("\n if you want to withdraw or deposit press 1 else 0\n");
    int t;
    scanf("%d",&t);

    if(t==1)
        manage();

    while(n==1)
    {
        printf("\n\n\n\n\n\t\t\t\t\tDo u want to continue doing transaction" );
        printf("\n1.)Yes");
        printf("\n2.)No");
        scanf("\n%d",&n);

        if(n==1)
        {
            manage();
        }
    }
}
}
