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
                                      
                                      
 #include <iostream>

using namespace std;
double f_u(double t, double u, double v) { 
    return v;
}

double f_v(double t, double u, double v) { 
    return -u;
}

int main()
{
    double a = 0, b = 10, h = 0.01, n = (b - a) / h, t = 0, y = 0, u = 0, v = 1;

    for (int i = 0; i < n; i++) {
        
        u += h * f_u(t, u, v);
        v += h * f_v(t, u, v);

        t += h;
        
        std::cout << u << "\t" << v << std::endl;
    }
    
    return 0;
}


#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;
const double PI = 3.141592653589793;


# Runge Kutta automatic step system 
double f1(double t, double u, double v) {
	return 0.1 * cos(t) - fabs(u) * (v + u);
}

double f2(double t, double u, double v) {
	return v + 10. * cos(t);
}

int main() {

	double t = 0; double T = 50 * PI; double h = 0.01; double n = (T - t) / h;
	double u = 0, v = 0;
	double K1_u, K2_u, K3_u, K4_u, K5_u, K6_u, K7_u, K1_v, K2_v, K3_v, K4_v, K5_v, K6_v, K7_v;
	double u_new, v_new, u_new_star, v_new_star, error, error_u, error_v, factmax = 1.3, factmin = 0.7, fac = 0.9, tol = 1e-7;

	for (int i = 0; i < n; i++) {

		if (t + h > T) {

			h = T - t;

		}

		K1_u = f2(t, u, v);
		K1_v = f1(t, u, v);

		K2_u = f2(t + 1. / 5 * h, u + 1. / 5 * h * K1_u, v + 1. / 5 * h * K1_v);
		K2_v = f1(t + 1. / 5 * h, u + 1. / 5 * h * K1_u, v + 1. / 5 * h * K1_v);

		K3_u = f2(t + 3. / 10 * h, u + 3. / 40 * h * K1_u + 9. / 40 * h * K2_u, v + 3. / 40 * h * K1_v + 9. / 40 * h * K2_v);
		K3_v = f1(t + 3. / 10 * h, u + 3. / 40 * h * K1_u + 9. / 40 * h * K2_u, v + 3. / 40 * h * K1_v + 9. / 40 * h * K2_v);

		K4_u = f2(t + 4. / 5 * h, u + 44. / 45 * h * K1_u - 56. / 15 * h * K2_u + 32. / 9 * h * K3_u, v + 44. / 45 * h * K1_v - 56. / 15 * h * K2_v + 32. / 9 * h * K3_v);
		K4_v = f1(t + 4. / 5 * h, u + 44. / 45 * h * K1_u - 56. / 15 * h * K2_u + 32. / 9 * h * K3_u, v + 44. / 45 * h * K1_v - 56. / 15 * h * K2_v + 32. / 9 * h * K3_v);

		K5_u = f2(t + 8. / 9 * h, u + 19372. / 6561 * h * K1_u - 25360. / 2187 * h * K2_u + 64448. / 6561 * h * K3_u - 212. / 729 * h * K4_u, v + 19372. / 6561 * h * K1_v - 25360. / 2187 * h * K2_v + 64448. / 6561 * h * K3_v - 212. / 729 * h * K4_v);
		K5_v = f1(t + 8. / 9 * h, u + 19372. / 6561 * h * K1_u - 25360. / 2187 * h * K2_u + 64448. / 6561 * h * K3_u - 212. / 729 * h * K4_u, v + 19372. / 6561 * h * K1_v - 25360. / 2187 * h * K2_v + 64448. / 6561 * h * K3_v - 212. / 729 * h * K4_v);

		K6_u = f2(t + h, u + 9017. / 3168 * h * K1_u - 355. / 33 * h * K2_u + 46732. / 5247 * h * K3_u + 49. / 176 * h * K4_u - 5103. / 18656 * h * K5_u, v + 9017. / 3168 * h * K1_v - 355. / 33 * h * K2_v + 46732. / 5247 * h * K3_v + 49. / 176 * h * K4_v - 5103. / 18656 * h * K5_v);
		K6_v = f1(t + h, u + 9017. / 3168 * h * K1_u - 355. / 33 * h * K2_u + 46732. / 5247 * h * K3_u + 49. / 176 * h * K4_u - 5103. / 18656 * h * K5_u, v + 9017. / 3168 * h * K1_v - 355. / 33 * h * K2_v + 46732. / 5247 * h * K3_v + 49. / 176 * h * K4_v - 5103. / 18656 * h * K5_v);

		K7_u = f2(t + h, u + 35. / 384 * h * K1_u + 500. / 1113 * h * K3_u + 125. / 192 * h * K4_u - 2187. / 6784 * h * K5_u + 11. / 84 * h * K6_u, v + 35. / 384 * h * K1_v + 500. / 1113 * h * K3_v + 125. / 192 * h * K4_v - 2187. / 6784 * h * K5_v + 11. / 84 * h * K6_v);
		K7_v = f1(t + h, u + 35. / 384 * h * K1_u + 500. / 1113 * h * K3_u + 125. / 192 * h * K4_u - 2187. / 6784 * h * K5_u + 11. / 84 * h * K6_u, v + 35. / 384 * h * K1_v + 500. / 1113 * h * K3_v + 125. / 192 * h * K4_v - 2187. / 6784 * h * K5_v + 11. / 84 * h * K6_v);

		u_new = u + h * (35. / 384 * K1_u + 500. / 1113 * K3_u + 125. / 192 * K4_u - 2187. / 6784 * K5_u + 11. / 84 * K6_u);
		v_new = v + h * (35. / 384 * K1_v + 500. / 1113 * K3_v + 125. / 192 * K4_v - 2187. / 6784 * K5_v + 11. / 84 * K6_v);

		u_new_star = u + h * (5179. / 57600 * K1_u + 7571. / 16695 * K3_u + 393. / 640 * K4_u - 92097. / 339200 * K5_u + 187. / 2100 * K6_u + 1. / 40 * K7_u);
		v_new_star = v + h * (5179. / 57600 * K1_v + 7571. / 16695 * K3_v + 393. / 640 * K4_v - 92097. / 339200 * K5_v + 187. / 2100 * K6_v + 1. / 40 * K7_v);

		error_u = fabs(u_new - u_new_star);
		error_v = fabs(v_new - v_new_star);
		error = max(error_u, error_v);

		if (error <= tol) {

			t += h;
			u = u_new;
			v = v_new;

			cout << u << "\t" << v << endl;

			if (fabs(T - t) <= 1e-13) 
				break;

			h = h * min(factmax, max(factmin, fac * pow(tol / error, 1./6)));

		}

		else {

			h = h * min(factmax, max(factmin, fac * pow(tol / error, 1./6)));
			i--;
		}

	}

	return 0;
}
