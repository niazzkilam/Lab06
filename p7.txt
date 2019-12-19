#include <stdio.h>
#include <stdlib.h>

struct VecInt
{
    int* data;
    int sz;
    int cp;
};

void VecInt_createEmpty(struct VecInt* this)
{
    this->data = NULL;
    this->sz = 0;
    this->cp = 0;
}

void VecInt_createOfSize(struct VecInt* this, int size, int initValue)
{
    this->data = malloc(sizeof(int) * size);
    this->sz = size;
    this->cp = 0;
    for (int i = 0; i < this->sz; ++i)
    {
        this->data[i] = initValue;
    }
}

void VecInt_pushBack(struct VecInt* this, int x)
{
    if (this->sz == this->cp)
    {
        this->cp = this->cp == 0 ? 1: 2 * this->cp;
        int* p = malloc(this->cp * sizeof(int));
        
        for (int i = 0; i < this->sz; ++i)
        {
            p[i] = this->data[i];
        }
        
        free(this->data);
        this->data = p;
    }
    this->data[this->sz] = x;
    ++this->sz;
}

void VecInt_destroy(struct VecInt* this)
{
    free(this->data);
    this->data = NULL;
    this->sz = 0;
    this->cp = 0;
}

void printArray(int* beg, int* end)
{
    while (beg != end)
    {
        printf("%d ", *beg++);
    }
    printf("\n");
}

void reverse(int* beg, int* end)
{
    if (beg == end)
        return;
    
    for (;;)
    {
        if (--end == beg) break;
        
        int t = *beg;
        *beg = *end;
        *end = t;
        
        if (++beg == end) break;
    }
}

void readSequenceAndReverse01()
{
    printf("number of int values: ");
    int n;
    scanf("%d", &n);
    
    struct VecInt v;
    VecInt_createOfSize(&v, n, 0);
 
    printf("Enter %d int values:\n", v.sz);
    
    for (int i = 0; i < v.sz; ++i)
    {
        scanf("%d", &v.data[i]);
    }
    
    reverse(v.data, v.data + v.sz);
    
    printArray(v.data, v.data + v.sz);
        
    VecInt_destroy(&v);
}

void readSequenceAndReverse02()
{
    struct VecInt v;
    VecInt_createEmpty(&v);
 
    printf("Enter arbitrary amount of numbers\n");
    
    int x;
    while (scanf("%d", &x) == 1)
    {
        VecInt_pushBack(&v, x);
    }
    
    reverse(v.data, v.data + v.sz);
    
    printArray(v.data, v.data + v.sz);
        
    VecInt_destroy(&v);
}

int main(void)
{
    readSequenceAndReverse01();
    readSequenceAndReverse02();
    
    return 0;
}