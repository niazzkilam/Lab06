#include <stdio.h>

void printArray(int* p, int len)
{
    int* e = p + len;
    while (p != e)
    {
        printf("%d ", *p++);
    }
    printf("\n");
}

void printArray2(int* p, int len)
{
    for (int i = 0; i < len; ++i)
    {
        printf("%d ", p[i]);
    }
    printf("\n");
}

int main(void)
{
    int a[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int b[] = {10, 20, 30, 40, 50};
    
    printArray(a, sizeof(a) / sizeof(*a));
    printArray(&b[0], sizeof(b) / sizeof(b[0]));
    
    return 0;
}