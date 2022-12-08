# Runge-Kutta-5
#include <iostream>

using namespace std;
double f(double t, double y) { 
    return 2 * t;
}

int main()
{
    double a = 0, b = 1000, h = 0.01, n = (b - a) / h, t = 0, y = 0;
    double K1, K2, K3, K4, K5, K6, K7;
    
    for (int i = 0; i < n; i++) {
        K1 = f(t, y);
        K2 = f(t + 1. / 5 * h, y + 1. / 5 * h * K1);
        K3 = f(t + 3. / 10 * h, y + 3. / 40 * h * K1 + 9. / 40 * h * K2);
        K4 = f(t + 4. / 5 * h, y + 44. / 45 * h * K1 - 56. / 15 * h * K2 + 32. / 9 * h * K3);
        K5 = f(t + 8. / 9 * h, y + 19372. / 6561 * h * K1 - 25360. / 2187 * h * K2 + 64448. / 6561 * h * K3 - 212. / 729 * h * K4);
        K6 = f(t + h, y + 9017. / 3168 * h * K1 - 355. / 33 * h * K2 + 46732. / 5247 * h * K3 + 49. / 176 * h * K4 - 5103. / 18656 * h * K5);
        K7 = f(t + h, y + 35. / 384 * h * K1 + 500. / 1113 * h * K3 + 125. / 192 * h * K4 - 2187. / 6784 * h * K5 + 11. / 84 * h * K6);
        y += h * (35. / 384 * K1 + 500. / 1113 * K3 + 125. / 192 * K4 - 2187. / 6784 * K5 + 11. / 84 * K6);
        t += t + h;
    
        std::cout << y << std::endl;
    }
    return 0;
}

# Euler
                                 
#include <iostream>

using namespace std;
double f(double t) { 
    return 2 * t;
}

int main()
{
    double a = 0, b = 10, h = 0.01, n = (b - a) / h, t = 0, y = 0;

    for (int i = 0; i < n; i++) {
        
        y += h * f(t);
        t += h;
        
        // std::cout << y << std::endl;
    }
    
    return 0;
}
