#include <algorithm>
#include <iostream>


using namespace std;

class VecInt
{
    int* data;
    int sz;
    int cp;
    
public:
    VecInt()
        : data(nullptr)
        , sz(0)
        , cp(0)
    {
    }

    explicit VecInt(int size, int initValue = 0)
        : data(new int[size])
        , sz(size)
        , cp(size)
    {
        for (int i = 0; i < sz; ++i)
        {
            data[i] = initValue;
        }
    }

    ~VecInt()
    {
        delete[] data;
    }
 
    int operator[](int index) const
    {
        return data[index];
    }
    
    int& operator[](int index)
    {
        return data[index];
    }

    int size() const
    {
        return sz;
    }
    
    const int* begin() const
    {
        return data;
    }
    
    const int* end() const
    {
        return data + sz;
    }
    
    int* begin()
    {
        return data;
    }
    
    int* end()
    {
        return data + sz;
    }
    
    void pushBack(int x)
    {
        if (sz == cp)
        {
            cp = cp == 0 ? 1: 2 * cp;
            int* p = new int[cp];
            
            for (int i = 0; i < sz; ++i)
            {
                p[i] = data[i];
            }
            
            delete[] data;
            data = p;
        }
        data[sz++] = x;
    }
};

void readSequenceAndReverse01()
{
    cout << "number of int values: ";
    int n;
    cin >> n;
    
    VecInt v(n);
    cout << "Enter " << n << " int values:\n";
    
    for (int i = 0; i < v.size(); ++i)
    {
        cin >> v[i];
    }
    
    reverse(begin(v), end(v));
    
    for (auto e : v)
    {
        cout << e << " ";
    }
    cout << "\n";
}

void readSequenceAndReverse02()
{
    VecInt v;
    
    cout << "Enter arbitrary amount of numbers\n";
    
    int x;
    while (cin >> x)
    {
        v.pushBack(x);
    }
    
    reverse(begin(v), end(v));
    
    for (auto e : v)
    {
        cout << e << " ";
    }
    cout << "\n";
}

int main()
{
    readSequenceAndReverse01();
    readSequenceAndReverse02();
}