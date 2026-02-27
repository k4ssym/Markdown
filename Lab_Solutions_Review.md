# CSCI 151 Laboratory Solutions Review
**Student:** Kassymzhomart Shubay  
**Class:** CL1  

This document contains all laboratory solutions for comprehensive review.

---

## Computer Lab 1 (CLab1)

### Task 1: Space Travel Time Calculator
**Problem:** Calculate the time needed to travel a given distance at a specified speed, converting the result to years, months, days, and hours.

```c
#include <stdio.h>

int main () {
    long long distance = 4194109984;
    long long speed;
    scanf("%lld", &speed);
    long long time = distance / speed;
    int a, b, c, d;
    a = time / (24 * 360);
    time = time % (24 * 360);
    b = time / (24 * 30);
    time = time % (24 * 30);   
    c = time / 24;
    time = time % 24;
    d = time;
    printf("%d years, %d months, %d days, %d hours", a, b, c, d);

}
```

### Task 2: Service Window Queue Simulation
**Problem:** Calculate total waiting time for clients in a queuing system with multiple service windows.

```c
#include <stdio.h>

int main () {
    int w, t;
    long long n;
    printf("Enter the number of windows: ");
    scanf("%d", &w);
    printf("Enter the time to serve a client in minutes: ");
    scanf("%d", &t);
    printf("Enter the number of clients: ");
    scanf("%lld", &n);
    long long people = n / w;
    long long total_time = people * t;

    long long years = total_time / (60 * 24 * 360);
    total_time = total_time % (60 * 24 * 360);

    long long months = total_time / (60 * 24 * 30);
    total_time = total_time % (60 * 24 * 30);

    long long days = total_time / (60 * 24);
    total_time = total_time % (60 * 24);

    long long hours = total_time / 60;
    total_time = total_time % 60;

    long long minutes = total_time;

    printf("years - %lld\n", years);
    printf("months - %lld\n", months);
    printf("days - %lld\n", days);
    printf("hours - %lld\n", hours);
    printf("minutes - %lld\n", minutes);
}
```

---

## Computer Lab 2 (CLab2)

### Task 1: Taylor Series Sine Calculator
**Problem:** Calculate sine using Taylor series expansion up to 15 terms.

```c
#include <stdio.h>

int main () {
    const double pi = 3.14159265;
    int au;
    printf("Enter an angle: ");
    scanf("%d", &au);
    double a = au / (180 / pi);
    double res = 0.0;


    for (int i = 0; i < 15; i++) {
        double up = 1.0;
        double low = 1.0;
        if (i % 2 == 1) {
            up *= -1;
        }
        for (int j = 0; j < i; j++) {
            up *= a * a;
        }
        up = up * a;

        for (int k = 2 * i + 1; k >= 1; k--) {
            low *= k;
        }

        res += (up/low);
    }

    printf("The sine of %d is %.6f", au, res);
    return 0;

}
```

### Task 2: Sum of Even Digits
**Problem:** Extract and sum all even digits from a series of input numbers until 0 is entered.

```c
#include <stdio.h>

int main () {
    int in;
    printf("Enter n: ");
    scanf("%d", &in);

    while (in != 0) {
        int sum = 0;
        int zapaska = in;
        while (zapaska > 0){
            int k = zapaska % 10;
            while ((k & 1) == 0) {
                sum += k;
                break;
            }
            zapaska /= 10;
        }
        printf("Sum of evens: %d\n\n", sum);
        printf("Enter n: ");
        scanf("%d", &in);
    }
}
```

### Task 3: Diamond/Hourglass Pattern
**Problem:** Print a diamond or hourglass pattern using asterisks based on input size.

```c
#include <stdio.h> 

int main () {
    int w;
    printf("Enter n: ");
    scanf("%d", &w);

    int stars = w;
    int spaces = 0;

    for (int i = 0; i < w; i++) {
        for (int j = 0; j < spaces; j++) {
            printf(" ");
        }

        for (int j = 0; j < stars; j++) {
            printf("*");
        }
        printf("\n");

        if (i < w / 2) {
            stars -= 2;
            spaces++;
        } else {
            stars += 2;
            spaces --;
        }
    }

}
```

---

## Computer Lab 3 (CLab3)

### Task 1: Random Number Comparison
**Problem:** Generate random triplets and determine their ordering relationship.

```c
#include <stdio.h>
#include <time.h>
#include <stdlib.h>

int main() {    
    srand(time(NULL));

    unsigned int a, b, c;

    for (int i = 0; i < 5; i++) { //you asked 5 times, here it is
        a = rand() % 41 + 10;
        b = rand() % 41 + 10;
        c = rand() % 41 + 10;                       

        printf("a=%u, b=%u, c=%u | ", a, b, c);
    
        if (a > b && b > c) { //три вариации трех букв ABC
            printf("a > b > c\n");
        } else if (a > c && c > b) { //ACB
            printf("a > c > b\n");
        } else if (b > a && a > c) { //BAC
            printf("b > a > c\n");
        } else if (b > c && c > a) { //BCA
            printf("b > c > a\n");
        } else if (c > a && a > b) { //CAB
            printf("c > a > b\n");
        } else  {
            printf("c > b > a\n"); //CBA
        }
    }
    return 0;
}
```

### Task 2: Digit Multiplication by Factor
**Problem:** Multiply each digit of a number by a given factor and print the result.

```c
#include <stdio.h>
#include <time.h>
#include <stdlib.h>

int main() {    
    size_t n, f;
    printf("Enter n: ");
    scanf("%zu", &n);
    printf("Enter a factor: "); 
    scanf("%zu", &f);
    printf("New number: ");

    if (n == 0 || f == 0) { //if input was 123 and factor 0 it printed 000
        printf("0");
    }
    else {
        size_t div = 1;
        size_t pamyat = n;

        while (pamyat >= 10) { // for divisor
            pamyat = pamyat / 10;
            div = div * 10;
        }
        while (div > 0) { //we get every digit
            size_t digit = n / div;
            printf("%zu", digit * f);
            n = n % div;
            div = div / 10;
        }
    }
    printf("\n");   
    return 0;
}
```

### Lab Quiz: Diamond Pattern Generator
**Problem:** Create a diamond pattern that expands and contracts symmetrically.

```c
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);

    for (int i = 0 ; i <= n / 2; i++) {

        for (int j = 0; j < i; j++) printf(" ");
        for (int j = 0; j < n - 2 * i; j++) printf("*");
        printf("\n");
    }
    for (int i = n / 2 - 1; i >= 0; i--) {
        for (int j = 0; j < i; j++) printf(" ");
        for (int j = 0; j < n - 2 * i; j++) printf("*");
        printf("\n");
    }


    return 0;
}
```

---

## Computer Lab 4 (CLab4)

### Task 1: Car Tax Calculator
**Problem:** Read car data from file and calculate taxes based on engine volume, year, and government rates.

```c
#include <stdio.h>

int main (){
    FILE * fin = fopen("cars.txt", "r");
    if (fin == NULL) {
        printf("Error opening file!");
        return 1;   
    }   

    char brand [50];
    char model [50];
    int year;
    double volume;
    int tax = 0;
    printf("%-8s\t%-24s\t%s\t%-20s\t%s\n", "Brand", "Model", "Year", "Engine Volume (cm3)", "Tax in tenge");
    char header [200];
    fgets(header, 200, fin);
    int rate = 3932;
    while(fscanf(fin, "%s\t%[^\t]\t%d\t%lf", brand, model, &year, &volume) != EOF) {
        int V = (int)(volume * 1000 + 0.5);
        int base = 0;
        int limit = 0;
        int excess = 0;
        if (V <= 3000) {
            if (V <= 1100) {
                base = 1;
                limit = 0;
            } else if (V <= 1500) {
                base = 2;
                limit = 1100;
            } else if (V <= 2000) {
                base = 3;
                limit = 1500;
            } else if (V <= 2500) {
                base = 6;
                limit = 2000;
            } else {
                base = 9;
                limit = 2500;
            }
        } else {
            if (year >= 2014) {
                if (V <= 3200) {
                    base = 35;
                    limit = 3000;
                } else if (V <= 3500) {
                    base = 46;
                    limit = 3200;
                } else if (V <= 4000) {
                    base = 66;
                    limit = 5000;
                } else if (V <= 5000) {
                    base = 130;
                    limit = 4000;
                } else {
                    base = 200;
                    limit = 5000;
                }
            } else {
                if (V <= 4000) {
                    base = 15;
                    limit = 3000;
                } else {
                    base = 117;
                    limit = 4000;
                }
            }
        }
        int tax = base * rate;

        if (V > 1500) {
            excess = V - limit;
            tax = tax + excess * 7;
        }

        printf("%-8s\t%-24s\t%d\t%-20.3f\t%d tg\n", brand, model, year, volume, tax);
        

    }



    fclose(fin);
    return 0;
}
```

---

## Computer Lab 5 (CLab5)

### Task 1: Array Element Frequency Counter
**Problem:** Count frequency of elements in array passed via command line arguments, avoiding duplicate output.

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>



int main (int argc, char *argv[]) {
    int i, j, k;
    int n = argc - 1;
    int arr[n];
    printf("Array elements: ");
    
    for (i = 0; i < n; i++) { //convert each char to int
        arr[i] = atoi(argv[i + 1]);
        printf("%d ", arr[i]);
    }
    printf("\n");

    for (i = 0; i < n; i++) { //get every element
        _Bool printed = 0;
        for (j = 0; j < i; j++) {
            if (arr[i] == arr[j]) // check
                printed = 1;
        }
        if (printed)
            printf("We found %d but it was printed before.\n", arr[i]);
        else {
            int count = 0;
            for (k = 0; k < n; k++) {
                if (arr[i] == arr[k]) {
                    count++;
                }
            }
            printf("Element %d occurred %d times.\n", arr[i], count);
        }
    }



    return 0;
}
```

### Task 2: Word Search in Grid
**Problem:** Search for a word horizontally in a 10x10 character grid loaded from file.

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

int main(int argc, char *argv[]) {
    if (argc < 3) { //check to see if its >3
        printf("Missing arguments.\n");
        return 1;
    }
    FILE * fin = fopen(argv[1], "r");
    if (fin == NULL) { //from the lab manual
        printf("Couldn't open the file.\n");
        return 1;
    }
    char table[10][10];

    for (int i = 0; i < 10; i++) { //creating table 10 x 10
        for (int j = 0; j < 10; j++) {
            int c = fgetc(fin);
            while (c == '\n') {
                c = fgetc(fin);
            }
            table[i][j] = (char)c;
        }
    }
    fclose(fin);

    char word[50];
    int length = 0;
    for (int i = 0; argv[2][i] != '\0'; i++) { //the needed word as its the 2nd argument
        word[i] = argv[2][i];
        length++;
    }
    word[length] = '\0';
    printf("  0123456789\n");
    for (int i = 0; i < 10; i++) { //table rendering
        printf("%d ", i);
        for (int j = 0; j < 10; j++) {
            printf("%c", table[i][j]);
        }
        printf("\n");
    }
    bool found = 0;
    int row = -1, column = -1;
    for (int i = 0; i < 10; i++) { //vertical checking
        for (int j = 0; j < 10; j++) {
            if (table[i][j] == word[0]) {
                int j2 = j;
                int k = 0;
                bool match = 1;
                while (word[k] != '\0') { //when you are done with the line
                    if (j2 >= 10) { // if your j2 is bigger then the length of the table :(
                        match = 0;
                    } else {
                        if (table[i][j2] != word[k]) {
                            match = 0;
                        }
                    }
                    j2++;
                    k++;
                }
                if (match) { //if true then yeaaah
                    found = 1;
                    row = i;
                    column = j;
                }
            }
        }

    }


    if (found)
        printf("the word %s is found at %d,%d\n", word, row, column);
    else {
        printf("the word %s is not found\n", word);
    }

    return 0;

}
```

---

## Programming Assignment (PA)

### Task 1: File-Based Arithmetic Operations
**Problem:** Read numbers and operator from input file, perform operations, write results to output file.

```c
#include <stdio.h>

int main (){

    FILE * in = fopen("input.txt", "r");

    int N;
    fscanf(in, "%d", &N);
    int numbers[N];
    for (int i = 0; i < N; i++) { //read the numbers into arr
        fscanf(in, "%d", &numbers[i]);
    }
    char operator;
    int the;
    fscanf(in, " %c %d", &operator, &the);

    FILE * out = fopen("output.txt", "w");

    for (int i = 0; i < N; i++) {
        if (operator == 43) { // ASCII +
            fprintf(out, "%d\n", numbers[i] + the);
        } else if (operator == 45) { // ASCII -
            fprintf(out, "%d\n", numbers[i] - the);
        } else if (operator == 42) { // ASCII *
            fprintf(out, "%d\n", numbers[i] * the);
        } else if (operator == 47) {// ASCII /
            if (numbers[i] % the == 0) { //.0 rendering
                fprintf(out, "%d\n", numbers[i] / the);
            } else {
                fprintf(out, "%g\n", (double)(numbers[i]) / the);
            }
        }


    }


    fclose(in);
    fclose(out);


    return 0;
}
```

### Task 2: Number Guessing Game
**Problem:** Generate random number between 100-500, give user 8 attempts to guess with hints.

```c
#include <stdio.h>
#include<stdlib.h>
#include<time.h>

int main() {


    srand(time(0));
    int randomNumber = 100 + rand() % 401;
    printf("I generated a random number between 100 and 500.\n");
    printf("Your guess?\n");
    int input;
    for (int i = 0; i <= 8; i++) {
        scanf("%d", &input);
        if (input == randomNumber) { //sovpalo
            printf("Yes! You have found the correct number in %d guesses.\n", i);
            return 0;
        } else if (input > randomNumber) { //its lower
            printf("Less\n");
        } else { //its not lower
            printf("More\n");
        }



    }
    printf("Game over! You had 8 guesses. The number was %d.\n", randomNumber);




    return 0;
}
```

### Task 3: String Pattern Removal
**Problem:** Remove all occurrences of a substring from input string and print the cleaned result.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main () {

    char input[300];
    char word[100];
    scanf("%s", input);
    scanf("%s", word);
    int input_k = strlen(input);
    int word_k = strlen(word);
    
    for (int i = 0; i < input_k; ) { 
        _Bool yes = 1; 
        //we check if our target matches some part of it 
        for (int j = 0; j < word_k; j++) {
            if (input[i + j] != word[j]) {
                yes = 0;
                break;
            }
        }
        if (yes) { // if match, then go on
            i = i + word_k;
        } else { //if no match, print what u have
            printf("%c", input[i]);
            i++;
        }
    }
    printf("\n");

    return 0;
}
```

---

## Summary

This review document contains **14 programming tasks** across 6 different laboratory assignments:

- **CLab1:** 2 tasks (time calculations, queue simulation)
- **CLab2:** 3 tasks (Taylor series, digit operations, patterns)  
- **CLab3:** 3 tasks (random comparisons, digit multiplication, pattern quiz)
- **CLab4:** 1 task (file processing with tax calculations)
- **CLab5:** 2 tasks (array processing, word search)
- **PA:** 3 tasks (file I/O, game programming, string manipulation)

**Key Programming Concepts Covered:**
- Mathematical calculations and algorithms
- File I/O operations
- String manipulation and pattern matching
- Dynamic arrays and command-line arguments
- Random number generation
- Complex control structures and loops
- Data type conversions and formatting