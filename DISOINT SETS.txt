#include<stdio.h>
struct DISJOINTSET
{
    int parent[10];
    int rank[10];
    int n;
}dis;
void makeSet()
{
    for(int i=0;i<dis.n;i++)
    {
        dis.parent[i]=i;
        dis.rank[i]=0;
    }
}
void displaySet()
{
    printf("\n PARENT ARRAY \n");
    for(int i=0;i<dis.n;i++)
    {
        printf("%d",dis.parent[i]);
    }
    printf("\n RANK ARRAY \n");
    for(int i=0;i<dis.n;i++)
    {
        printf("%d",dis.rank[i]);
    }
    printf("\n");
}
int find(int x)
{
    if(dis.parent[x]!=x)
    {
        dis.parent[x]=find(dis.parent[x]);
    }
    return dis.parent[x];
}
void setunion(int x,int y)
{
    int xset=find(x);
    int yset=find(y);
    if(xset==yset)
        return;
    if(dis.rank[xset]<dis.rank[yset])
    {
        dis.parent[yset]=xset;
        dis.rank[yset]=-1;
    }
    else
    {
        dis.parent[yset]=xset;
        dis.rank[xset]=dis.rank[xset]+1;
        dis.rank[yset]=-1;
    }
}
int main()
{
    int x,y,z,a[20];
    printf("ENTER NO OF ELEMENTS : ");
    scanf("%d",&dis.n);
    makeSet();
    int ch,wish;
    do{
        printf("\n MENU \n");
        printf("\n 1.UNION\n 2.FIND\n 3.DISPLAY \n");
        printf("ENTER CHOICE : ");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1:printf("\nENTER ELEMENTS TO PERFOR UNION : ");
            scanf("%d%d",&x,&y);
            setunion(x,y);
            break;
            
            case 2:printf("ENTER ELEMENTS TO CHECK IF CONNECTED COMPONENTS : ");
            scanf("%d%d",&x,&y);
            if(find(x)==find(y))
            printf("CONNECTED COMPONENTS\n ");
            else
            printf("NOT CONNECTED");
            break;
            case 3:displaySet();
            break;
        }
        printf("\nDO YOU WANT TO CONTINUE?(1/0)  ");
        scanf("%d",&wish);
    }while(wish==1);
    return 0;
}