// 4/2  
#include <iostream>
using namespace std;
int main() {
    // initialize an array
    int data[50] = {
        42, 7, 88, 12, 55, 1, 93, 22, 67, 34,
        15, 78, 4, 60, 29, 82, 45, 11, 99, 3,
        50, 26, 71, 18, 95, 6, 38, 84, 52, 10,
        63, 21, 8, 74, 49, 31, 87, 5, 59, 14,
        91, 33, 76, 2, 47, 68, 25, 80, 19, 56
    };

    // Analyze reverse order pairs (determine current state)
    int inversions = 0;
    for (int i = 0; i < 49; i++) {
        for (int j = i + 1; j < 50; j++) {
            if (data[i] > data[j]) inversions++;
        }
    }

    // Decision logic (50 * 49/2=1225 is the maximum number of reverse order pairs for 50 numbers)
    // Set 20%，80% as the threshold，1225*20%=245， 1225*80%=980
    if (inversions < 245) {
        //Insertion sorting 
        cout << ">> Best case distribution. Selection: Insertion Sort" << endl;
        for (int i = 1; i < 50; i++) {
            int key = data[i];
            int j = i - 1;
            while (j >= 0 && data[j] > key) {
                data[j + 1] = data[j];
                j--;
            }
            data[j + 1] = key;
        }
    } else if (inversions > 980) {
        //Insertion sorting
        cout << ">> Worst case distribution. Selection: Insertion Sort" << endl;
        for (int i = 1; i < 50; i++) {
            int key = data[i];
            int j = i - 1;
            while (j >= 0 && data[j] > key) {
                data[j + 1] = data[j];
                j--;
            }
            data[j + 1] = key;
        }
    else {
        //Selection sorting
        cout << ">> Average case distribution. Selection: Insertion Sort" << endl;
        for (int i = 0; i < 49; i++) {
            int min_idx = i;
            for (int j = i + 1; j < 50; j++) {
                if (data[j] < data[min_idx]) min_idx = j;
            }
            int temp = data[min_idx];
            data[min_idx] = data[i];
            data[i] = temp;
        }
    }

    for (int i = 0; i < 50; i++) cout << data[i] << " ";
    
    return 0;
}
}

Best Case: Inversion Ratio 20%. The array is nearly sorted.  
Worst Case: Inversion Ratio 80%. The array is nearly or strictly descending.  
Average Case: Inversion Ratio between 20 to 80. The array is random or "messy."  
Reasoning Behind the Assumption: If the ratio is low, most elements are already near their destination.Selection Sort performs the same number of comparisons regardless of the input.It is superior in one specific metric: swaps. It performs at most O(n)swaps, whereas Insertion Sort can perform O(n^2) assignments in a worst-case scenario.  