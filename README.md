//Author: manpreet kaur, dawinder kaur, Raghav Chpora
//Desrcription: quicksort.c
//created on : feb,13,2020

#include <stdio.h> /* used for standard input output */
#include <string.h> /*used for strcmp function for string */

// swap function declaration
static void swap(const char **arr, int x, int y)

/* This swaps two elements of &quot;arr&quot; indexed by "x" and "y" */

{
	const char *hold; // pointer set to a value hold
	printf("Swapping entry %d,'%s'to %d, and entry %d, '%s' to %d.\n", x,
			arr[x], y, y, arr[y], x);
	hold = arr[x];
	arr[x] = arr[y];
	arr[y] = hold; // swapping the array
}

static void quick_sort(const char **arr, int L, int R)

/* quick sort algorithm with const char as arr and two integer

 L and R */
{

	int pi; // integer specifies pi (center value) value of array
	int a;
	int b;
	const char *imp; // pointer imp
	/*if right character subtract left character equals to one then internal if statement run
	 which shows if array left and array right is greater than zero then swap function
	 will called*/
	if (R - L == 1) {
		if (strcmp(arr[L], arr[R]) > 0) {
			swap(arr, L, R);
		}
		return;
	}
	/* this statement pick a mid point for the pivot. */
	pi = (L + R) / 2;
	imp = arr[pi];
	/* swap function is called to put the pivot imp at the left of the list. */
	swap(arr, L, pi);
	a = L + 1;  // to move pointer to next left character
	b = R; // pointer to right character
	while (a < b) // when value a is less than b
	{
		while (a <= R && strcmp(arr[a], imp) < 0) {
			/* while statement used to leave the parts on the left of imp in place if
			 they are smaller than or equal to "imp". */
			a++; // move to next value on right side
		}
		while (b >= L && strcmp(arr[b], imp) > 0) {
			/* while statement used to leave the parts on the right of imp in place if

			 they are greater than imp. */
			b--; //move to previous value on left side
		}
		if (a <= b) {
			/* "array[i]" is greater than imp, and "array[j]" is
			 less than or equal to imp, so swap them. */
			swap(arr, a, b);
		}
	}
	/* swap function called to put the pivot imp back between the two sorted halves. */
	swap(arr, L, b);
	if (L < b - 1) {
		/* Sort the left half using this function recursively. */
		quick_sort(arr, L, b - 1);
	}
	if (b + 1 < R) {
		/* Sort the right half using this function recursively. */
		quick_sort(arr, b + 1, R);
	}
}
/*record array conatin constant character values to sort */
const char *records[] = { "Lovepreet Chouhan Rajpura", "Dawinder Virk Rajpura",
		"Manpreet Minhas Jalandar", "Raghav Chopra Pathankot",
		"Simranjeet Gill Moga", "Manjinder Toor Moga",
		"Baninder Chouhan Australia", "Amandeep Kaur Australia",
		"Harmanpreet Virk Calgary ", };
/* "n_records" is the number of names to sort. */

#define n_records (sizeof records)/(sizeof (const char *))
/* this function with for loop will prints the contents of "arr" with unknown size. */
static void print_array(const char **arr, int size) {
	int i;
	for (i = 0; i < size; i++) {
		printf("%d - %s\n", i, arr[i]);
// print the array after and before sorting
	}
	printf("\n");
}
// main function declaration
int main() {
	printf("List before sorting:\n\n");
	print_array(records, n_records);
//calling function print_array to print array before sorting
	quick_sort(records, 0, n_records - 1);
// calling quick_sort function to sort the alphabetical array
	printf("\nList after sorting:\n\n");
	print_array(records, n_records);
//calling function print_array to print array after sorting
	return 0;
}
