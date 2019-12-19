#include <algorithm>
#include <iostream>

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

    VecInt(const VecInt& other)
        : data(new int[other.sz])
        , sz(other.sz)
        , cp(other.cp)
    {
        for (int i = 0; i < sz; ++i)
        {
            data[i] = other.data[i];
        }
    }

    VecInt& operator=(const VecInt& other)
    {
        if (this == &other)
        {
            return *this;
        }

        VecInt t(other);

        this->swap(t);

        return *this;
    }

    ~VecInt()
    {
        delete[] data;
    }

    void swap(VecInt& other)
    {
        std::swap(data, other.data);
        std::swap(sz, other.sz);
        std::swap(cp, other.cp);
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
            cp = cp == 0 ? 1 : 2 * cp;
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

bool operator==(const VecInt& x, const VecInt& y)
{
    if (x.size() != y.size())
    {
        return false;
    }
    for (int i = 0; i < x.size(); ++i)
    {
        if (x[i] != y[i])
        {
            return false;
        }
    }
    return true;
}

bool operator!=(const VecInt& x, const VecInt& y)
{
    return !(x == y);
}

void isPalindromeWithCopyConstructor()
{
    using namespace std;
    
    cin.clear();

    VecInt v;

    cout << "Enter arbitrary amount of numbers\n";

    int x;
    while (cin >> x)
    {
        v.pushBack(x);
    }

    VecInt w = v;
    reverse(begin(w), end(w));

    cout << (v == w ? "Palindrome\n" : "Not a Palindrome\n");
}

void isPalindromeWithAssignment()
{
    using namespace std;
    
    cin.clear();

    VecInt v;

    cout << "Enter arbitrary amount of numbers\n";

    int x;
    while (cin >> x)
    {
        v.pushBack(x);
    }

    VecInt w;
    w = v;
    reverse(begin(w), end(w));

    cout << (v == w ? "Palindrome\n" : "Not a Palindrome\n");
}

int main()
{
    isPalindromeWithCopyConstructor();
    isPalindromeWithAssignment();
}