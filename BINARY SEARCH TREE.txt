#include<stdio.h>
struct treenode
{
    struct treenode *lchild;
    int data;
    struct treenode *rchild;
};
void main()
{
    int key,n,item,element;
    int ch;
    struct treenode *root;
        printf("__BINARY SEARCH TREE__\n");
    
    while(1)
    {
        printf("\n1.CREATE\n2.DELETE\n3.DISPLAY\n4.SEARCH\n5.EXIT");
        printf("\nENTER CHOICE : ");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1:
                   printf("ENTER NUMBER OF NODES : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
    {printf("\nENTER ELEMENT : ");
    scanf("%d",&item);
    CREATE(&root,item);
    }
    break;
    
    case 2:
           printf("\nENTER ELEMENT TO BE DELETED : ");
    scanf("%d",&element);
    DELETE(&root,element);
    break;
    
    case 3:
             printf("\n TREE IS \n");
    DISPLAY(root,1);
    break;
    
    case 4:
             printf("\nENTER ELEMENT TO BE SEARCHED : ");
    scanf("%d",&key);
    SEARCH(root,key);
    break;
    
    case 5:
            exit(0);
            
    default:
            printf("WRONG CHOICE");
        }
    }
    
   
   
    
}
CREATE(struct treenode **rt,int item)
{
    struct treenode *current=(*rt),*temp;
    if((*rt)==NULL)
    {
        (*rt)=(struct treenode*)malloc(sizeof(struct treenode));
        (*rt)->data=item;
        (*rt)->lchild=NULL;
        (*rt)->rchild=NULL;
        return;
    }
    while(current!=NULL)
    {
        if(item<current->data)
        {
            if(current->lchild!=NULL)
                current=current->lchild;
            else
            {
                temp=(struct treenode*)malloc(sizeof(struct treenode));
                current->lchild=temp;
                temp->data=item;
                temp->rchild=NULL;
                temp->lchild=NULL;
                return;
            }
        }
        else
        {
            if(item>current->data)
            {
                if(current->rchild!=NULL)
                    current=current->rchild;
                else
                {
                    temp=(struct treenode*)malloc(sizeof(struct treenode));
                    current->rchild=temp;
                    temp->data=item;
                    temp->rchild=NULL;
                    temp->lchild=NULL;
                    return;
                }
            }
        
            else
            {
                printf("\n WRONG DATA ");
                exit(0);
            }
        }
    }
}



DISPLAY(struct treenode *rt,int level)
{
    int i;
    if((rt)!=NULL)
    {
        DISPLAY((rt)->rchild,level+1);
        printf("\n");
        for(i=0;i<level;i++)
            printf(" ");
        printf("%d",(rt)->data);
        DISPLAY((rt)->lchild,level+1);
    }
}
SEARCH(struct treenode *rt,int k)
{
    int flag;
    if(rt==NULL)
    {
        printf("\n ERROR");
        flag=0;
    }
    else
    {
        if(k==rt->data)
        {
            printf("\n ELEMENT FOUND");
            flag=1;
        }
        else if(k<rt->data)
            SEARCH((rt)->lchild,k);
        else
            SEARCH((rt)->rchild,k);
    }
}
DELETE(struct treenode **rt,int element)
{
    struct treenode *current;
    if(*rt==NULL)
    {
        printf("ERROR");
        return;
    }
    if(element<(*rt)->data)
        DELETE(&((*rt)->lchild),element);
    else
    {
        if(element>(*rt)->data)
            DELETE(&((*rt)->rchild),element);
        else
        {
            current=(struct treenode*)malloc(sizeof(struct treenode));
            current=(*rt);
            if(current->rchild==NULL)
            {
                (*rt)=(*rt)->lchild;
                free(current);
            }
            else
            {
                current=(struct treenode*)malloc(sizeof(struct treenode));
                if(current->lchild==NULL)
                {
                    (*rt)=(*rt)->rchild;
                    free(current);
                }
                else
                {
                    current=(struct treenode*)malloc(sizeof(struct treenode));
                    current=(*rt)->rchild;
                    while(current->lchild!=NULL)
                        current=current->lchild;
                    current->lchild=(*rt)->lchild;
                    current=(*rt);
                    (*rt)=(*rt)->rchild;
                    free(current);
                }
            }
    }
}
}