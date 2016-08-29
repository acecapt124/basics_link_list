#include<stdio.h>
#include<malloc.h>
struct node
{
    int data;
    struct node *next;
};
typedef struct node node;
node *new_node(int value)
{
    node *temp;
    temp=(node*)malloc(sizeof(node));
    temp->data=value;
    temp->next=NULL;
    return temp;
}
void insertBeg(node **head,int value)
{
    node *temp=new_node(value);
    temp->next=*head;
    *head=temp;
}
void insertEnd(node **head,int value)
{   node *temp1=new_node(value);
    node *temp2=*head;
    if(temp2==NULL)
    {
    temp1->next=*head;
    *head=temp1;
    }
    else
    {
    while(temp2->next!=NULL)
    {
        temp2=temp2->next;
    }
    temp2->next=temp1;
    }
}
void insertBefore(node **head,int value1,int value2)
{
    node *temp1=new_node(value1);
    node *temp2=*head;
    node *prev;

        while(temp2->data!=value2)
        {   prev=temp2;
            temp2=temp2->next;
        }
        temp1->next=prev->next;
        prev->next=temp1;

}
void insertAfter(node **head,int value1,int value2)
{
    node *temp1=new_node(value1);
    node *temp2=*head;

        while(temp2->data!=value2)
        {
            temp2=temp2->next;
        }
        temp1->next=temp2->next;
        temp2->next=temp1;
}
void insertPos(node **head,int value1,int value2)
{
    node *temp1=new_node(value1);
    node *temp2=*head;
    node *prev;
    int i=0;
  while(i<value2-1)
  {
      prev=temp2;
      temp2=temp2->next;
  i++;
  }
        temp1->next=prev->next;
        prev->next=temp1;
}
void deleteNum(node **head,int value)
{
    node *temp=*head;
    node *prev;
    while(temp->data!=value)
    {
        prev=temp;
        temp=temp->next;
    }
    prev->next=temp->next;
    free(temp);
    temp=NULL;
}
void deleteBefore(node **head,int value)
{
    node *temp=*head;
    node *prev1,*prev2;
    while(temp->data!=value)
    {   prev1=prev2;
        prev2=temp;
        temp=temp->next;
    }
    prev1->next=prev2->next;
    free(prev2);
    prev2=NULL;
}
void deleteAfter(node **head,int value)
{
    node *temp=*head;
    node *temp1;
    while(temp->data!=value)
    {
        temp=temp->next;
    }
    temp1=temp->next;
    temp->next=temp1->next;
    free(temp1);
    temp1=NULL;
}
void deleteBeg(node **head)
{
    node *temp=*head;
    *head=temp->next;
    free(temp);
    temp=NULL;
}
void deleteEnd(node **head)
{
    node *temp=*head;
    node *prev;
    while(temp->next!=NULL)
   {    prev=temp;
       temp=temp->next;
   }
   prev->next=NULL;

}
void disp(node **head)
{

    if(head==NULL)
    {
        printf("Underflow");
    }
    node *temp=*head;
        while(temp->next!=NULL)
        {
            printf(" %d",temp->data);
            temp=temp->next;
        }
        printf(" %d",temp->data);
        printf("\n");
}
int main()
{   node *head=NULL;
    insertBeg(&head,5);
    disp(&head);
    insertBeg(&head,1);
    disp(&head);
    insertEnd(&head,4);
    disp(&head);
    insertEnd(&head,5);
    disp(&head);
    insertPos(&head,2,3);
    disp(&head);
    deleteNum(&head,2);
    disp(&head);
    deleteBefore(&head,4);
    disp(&head);
    deleteAfter(&head,1);
    disp(&head);
    insertAfter(&head,6,5);
    disp(&head);
    insertBefore(&head,3,5);
    disp(&head);
    deleteBeg(&head);
    disp(&head);
    deleteEnd(&head);
    disp(&head);
    return 0;
}
