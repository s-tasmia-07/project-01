#include <stdio.h>

// Display the array
void display(int arr[], int size) {
    if (size == 0) {
        printf("Array is empty.\n");
        return;
    }

    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Insert value
int insert(int arr[], int size, int value, int position) {
    if (position < 0 || position > size) {
        printf("Invalid position!\n");
        return size;
    }

    for (int i = size; i > position; i--) {
        arr[i] = arr[i - 1];
    }
    arr[position] = value;
    size++;
    display(arr, size);
    return size;
}

// Update value at position
void updateValue(int arr[], int size, int position, int newValue) {
    if (position < 0 || position >= size) {
        printf("Invalid position for update!\n");
    } else {
        arr[position] = newValue;
        display(arr, size);
    }
}

// Move value from one position to another
void updatePosition(int arr[], int size, int fromPos, int toPos) {
    if (fromPos < 0 || fromPos >= size || toPos < 0 || toPos >= size) {
        printf("Invalid position to move!\n");
        return;
    }

    int temp = arr[fromPos];
    if (fromPos < toPos) {
        for (int i = fromPos; i < toPos; i++) {
            arr[i] = arr[i + 1];
        }
    } else {
        for (int i = fromPos; i > toPos; i--) {
            arr[i] = arr[i - 1];
        }
    }
    arr[toPos] = temp;
    display(arr, size);
}

// Delete element at position
int deleteElement(int arr[], int size, int position) {
    if (position < 0 || position >= size) {
        printf("Invalid position to delete!\n");
        return size;
    }

    for (int i = position; i < size - 1; i++) {
        arr[i] = arr[i + 1];
    }
    size--;
    display(arr, size);
    return size;
}

// Sort using selection sort
void sort(int arr[], int size, int ascending) {
    for (int i = 0; i < size - 1; i++) {
        int selected = i;
        for (int j = i + 1; j < size; j++) {
            if ((ascending && arr[j] < arr[selected]) || (!ascending && arr[j] > arr[selected])) {
                selected = j;
            }
        }
        if (selected != i) {
            int temp = arr[i];
            arr[i] = arr[selected];
            arr[selected] = temp;
        }
    }
    printf("Array sorted in %s order:\n", ascending ? "ascending" : "descending");
    display(arr, size);
}

// Search value
void search(int arr[], int size, int value) {
    int found = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] == value) {
            printf("%d found at index %d\n", value, i);
            found = 1;
        }
    }
    if (!found) {
        printf("%d not found\n", value);
    }
}

// Main function with menu
int main() {
    int arr[100], size = 0, choice, value, position, fromPos, toPos;

    printf("Enter size: ");
    scanf("%d", &size);
    printf("Enter elements:\n");
    for (int i = 0; i < size; i++) {
        scanf("%d", &arr[i]);
    }

    while (1) {
        printf("\nMenu:\n");
        printf("1. Insert\n2. Update Value\n3. Update Position\n4. Delete\n5. Sort Ascending\n6. Sort Descending\n7. Search\n8. Display\n9. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to insert: ");
                scanf("%d", &value);
                printf("Enter position to insert at (0 to %d): ", size);
                scanf("%d", &position);
                size = insert(arr, size, value, position);
                break;

            case 2:
                printf("Enter position to update value (0 to %d): ", size - 1);
                scanf("%d", &position);
                printf("Enter new value: ");
                scanf("%d", &value);
                updateValue(arr, size, position, value);
                break;

            case 3:
                printf("Enter position to move from: ");
                scanf("%d", &fromPos);
                printf("Enter position to move to: ");
                scanf("%d", &toPos);
                updatePosition(arr, size, fromPos, toPos);
                break;

            case 4:
                printf("Enter position to delete: ");
                scanf("%d", &position);
                size = deleteElement(arr, size, position);
                break;

            case 5:
                sort(arr, size, 1);  // Ascending
                break;

            case 6:
                sort(arr, size, 0);  // Descending
                break;

            case 7:
                printf("Enter value to search: ");
                scanf("%d", &value);
                search(arr, size, value);
                break;

            case 8:
                display(arr, size);
                break;

            case 9:
                return 0;

            default:
                printf("Invalid choice. Try again.\n");
        }
    }

    return 0;
}
