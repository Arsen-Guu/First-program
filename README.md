#include <iostream>
#include <windows.h>
#include <ctime>
using namespace std;
double PCFreq = 0.0;
__int64 CounterStart = 0;
float* sortirovka(float* a, float count);
void StartCounter()
{
LARGE_INTEGER li;
if (!QueryPerformanceFrequency(&li))
std::cout « "QueryPerformanceFrequency failed!\n";

PCFreq = double(li.QuadPart) / 1000.0;

QueryPerformanceCounter(&li);
CounterStart = li.QuadPart;
}
double GetCounter()
{
LARGE_INTEGER li;
QueryPerformanceCounter(&li);
return double(li.QuadPart - CounterStart) / PCFreq;
}
int main()
{
setlocale(LC_ALL, "Russian");
srand(time(NULL));
int n = 0;
n = 1000;
cout « "Количество элементов в массиве : " « n;
cout « "\n";
float* u = new float[n];
for (int i = 0; i < n; i++)
{
u[i] = rand() / 1000.0f;
cout « u[i] « " ";
}
cout « endl;
StartCounter();
sortirovka(u, n);
std::cout « GetCounter() « "\n"; //It prints accurate time like 998
cout « "Отсортированный массив: ";
for (int i = 0; i < n; i++) {
cout « u[i] « " ";
}
cout « endl;
free(u);
return 0;
}
float* sortirovka(float* a, float count) {
for (int i = 0; i < count; i++)
for (int j = i; j < count; j++) {
if (a[i] > a[j]) {
float p = a[i];
a[i] = a[j];
a[j] = p;
}
}
return a;
}
