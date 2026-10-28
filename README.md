//Event-Management-System-
#include <stdio.h>
#include <string.h>

char eName[20][30];
char eDate[20][15];
char eVenue[20][30];
int eCount[20];
int totalEvents = 0;

char pName[100][30];
char pPhone[100][15];
int pEvent[100];
int totalPart = 0;

/* Add a new event */
void addEvent()
{
    if (totalEvents >= 20)
    {
        printf("Event limit reached!\n");
        return;
    }

    printf("Enter event name (no spaces): ");
    scanf("%29s", eName[totalEvents]);

    printf("Enter event date (DD-MM-YYYY): ");
    scanf("%14s", eDate[totalEvents]);

    printf("Enter event venue (no spaces): ");
    scanf("%29s", eVenue[totalEvents]);

    eCount[totalEvents] = 0;
    totalEvents++;

    printf("Event added successfully!\n");
}

/* Display all events */
void showEvents()
{
    int i;

    if (totalEvents == 0)
    {
        printf("No events available.\n");
        return;
    }

    for (i = 0; i < totalEvents; i++)
    {
        printf("\nEvent Number: %d\n", i + 1);
        printf("Name: %s\n", eName[i]);
        printf("Date: %s\n", eDate[i]);
        printf("Venue: %s\n", eVenue[i]);
        printf("Registrations: %d\n", eCount[i]);
    }
}

/* Register a participant */
void addParticipant()
{
    int no;

    if (totalEvents == 0)
    {
        printf("Please add an event first.\n");
        return;
    }

    if (totalPart >= 100)
    {
        printf("Participant limit reached!\n");
        return;
    }

    showEvents();

    printf("\nEnter event number: ");
    if (scanf("%d", &no) != 1)
    {
        printf("Invalid input!\n");
        return;
    }

    if (no < 1 || no > totalEvents)
    {
        printf("Wrong event number!\n");
        return;
    }

    printf("Enter participant name (no spaces): ");
    scanf("%29s", pName[totalPart]);

    printf("Enter phone number: ");
    scanf("%14s", pPhone[totalPart]);

    pEvent[totalPart] = no - 1;
    eCount[no - 1]++;
    totalPart++;

    printf("Participant registered successfully!\n");
}

/* Search participant by name */
void searchParticipant()
{
    char key[30];
    int i, found = 0;

    printf("Enter participant name to search: ");
    scanf("%29s", key);

    for (i = 0; i < totalPart; i++)
    {
        if (strcmp(pName[i], key) == 0)
        {
            printf("\nName: %s\n", pName[i]);
            printf("Phone: %s\n", pPhone[i]);
            printf("Event: %s\n", eName[pEvent[i]]);
            found = 1;
        }
    }

    if (found == 0)
    {
        printf("Participant not found.\n");
    }
}

/* Display event-wise report */
void report()
{
    int i, j;

    if (totalEvents == 0)
    {
        printf("No events available.\n");
        return;
    }

    for (i = 0; i < totalEvents; i++)
    {
        printf("\nEvent: %s\n", eName[i]);
        printf("Date: %s\n", eDate[i]);
        printf("Venue: %s\n", eVenue[i]);
        printf("Total registrations: %d\n", eCount[i]);

        for (j = 0; j < totalPart; j++)
        {
            if (pEvent[j] == i)
            {
                printf("Participant: %s, Phone: %s\n",
                       pName[j], pPhone[j]);
            }
        }
    }
}

/* Main menu */
int main()
{
    int choice;

    do
    {
        printf("\n===== EVENT MANAGEMENT SYSTEM =====\n");
        printf("1. Add Event\n");
        printf("2. Register Participant\n");
        printf("3. Show Events\n");
        printf("4. Search Participant\n");
        printf("5. Event Report\n");
        printf("0. Exit\n");

        printf("Enter your choice: ");

        if (scanf("%d", &choice) != 1)
        {
            printf("Invalid input. Please enter a number.\n");
            return 1;
        }

        if (choice == 1)
        {
            addEvent();
        }
        else if (choice == 2)
        {
            addParticipant();
        }
        else if (choice == 3)
        {
            showEvents();
        }
        else if (choice == 4)
        {
            searchParticipant();
        }
        else if (choice == 5)
        {
            report();
        }
        else if (choice == 0)
        {
            printf("Exiting program. Thank you!\n");
        }
        else
        {
            printf("Invalid choice. Try again.\n");
        }

    } while (choice != 0);

    return 0;
}
