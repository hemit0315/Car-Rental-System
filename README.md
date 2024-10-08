#include<stdio.h>
#include<string.h>

struct car {
    char name[50];
    int seats;
    float rent;
    char status[20];
};

void addcar(struct car cars[], int *n) 
{
    printf("\nEnter The details of the Car : \n");
    printf("\tName of Car : ");
    scanf("%s", cars[*n].name);
    printf("\n\tNo. of Seats in the Car :");
    scanf("%i", &cars[*n].seats);
    printf("\n\tRent of the Car : ");
    scanf("%f", &cars[*n].rent);
    strcpy(cars[*n].status, "Available");
    (*n)++;
    printf("\nCar added successfully!\n\n");
}

void display(struct car cars[], int n) 
{
    if (n == 0) 
	{
        printf("No cars available to display.\n");
        return;
    }
    for(int i = 0; i < n; i++) 
	{
        printf("\n\nCAR DETAILS : ");
        printf("\n\tCar %i\n", i + 1);
        printf("\tName of Car : %s\n", cars[i].name);
        printf("\tNo of Seats in the Car : %i\n", cars[i].seats);
        printf("\tRent of The Car : %.2f\n", cars[i].rent);
        printf("\tAvailability Status of the Car : %s\n\n", cars[i].status);
    }
}

void bookcar(struct car cars[], int n) 
{
    char carName[50];
    int found = 0, days;
    printf("\nEnter the name of the car you wish to book : ");
    scanf("%s", carName);
    for(int i = 0; i < n; i++) 
	{
        if(strcmp(cars[i].name, carName) == 0) 
		{
            found = 1;
            if(strcmp(cars[i].status, "Available") == 0) 
			{
                printf("\nCar is Available");
                printf("\nFor how many days do you wish to book the car? : ");
                scanf("%i", &days);
                printf("\nCar Booked Successfully for %i days \n", days);
                strcpy(cars[i].status, "Not Available");
            } 
			else 
			{
                printf("\nSorry The Car is not Available");
            }
            break; 
        }
    }
    if (!found) 
	{
        printf("Car not found!\n");
    }
}

void generatebill(struct car cars[], int n) 
{
    char carName[50];
    int days, found = 0;
    float total;
    printf("\nEnter the name of the car for the bill: ");
    scanf("%s", carName);
    for(int i = 0; i < n; i++) 
	{
        if(strcmp(cars[i].name, carName) == 0) 
		{
            found = 1;
            printf("\nEnter the number of days : ");
            scanf("%i", &days);
            total = cars[i].rent * days;
            printf("\n--- Bill Summary ---\n");
            printf("| Car Name | Days | Rent per Day | Total Amount |\n");
            printf("|----------|------|--------------|--------------|\n");
            printf("| %-8s | %-4d | %-13.2f | %-12.2f |\n", cars[i].name, days, cars[i].rent, total);
            printf("---------------------\n");
            break;
        }
    }
    if (!found) 
	{
        printf("Car not found!\n");
    }
}

int main() 
{
    struct car cars[10];
    int n = 0; 
    int choice;
    do 
	{
        printf("\nCar Rental System Menu:\n");
        printf("1. Add Car\n");
        printf("2. Display Cars\n");
        printf("3. Book Car\n");
        printf("4. Generate Bill\n");
        printf("5. Exit\n");
        printf("Choose an option: ");
        scanf("%d", &choice);
        switch (choice) 
		{
            case 1:
                if (n < 10) 
				{
                    addcar(cars, &n); 
                }
				else 
				{
                    printf("Cannot add more cars. Maximum limit reached.\n");
                }
                break;
            case 2:
                display(cars, n);
                break;
            case 3:
                bookcar(cars, n);
                break;
            case 4:
                generatebill(cars, n);
                break;
            case 5:
                printf("Exiting the system. Goodbye!\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 5);
    return 0;
}
