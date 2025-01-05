#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_DOCTORS 100
#define MAX_PATIENTS 100

// Struct for doctor information
typedef struct {
    char name[50];
    int adminNo;
    char phone[15];
    char email[50];
    char address[100];
    char gender[10];
} Doctor;

// Struct for patient information
typedef struct {
    char name[50];
    int patientID;
    char phone[15];
    char ailment[100];
} Patient;

Doctor doctors[MAX_DOCTORS] = {
    {"Dr. John Smith", 101, "123-456-7890", "john.smith@example.com", "123 Elm St, Springfield", "Male"},
    {"Dr. Emily Davis", 102, "987-654-3210", "emily.davis@example.com", "456 Oak St, Springfield", "Female"},
    {"Dr. Michael Brown", 103, "555-123-4567", "michael.brown@example.com", "789 Pine St, Springfield", "Male"},
    {"Dr. Sarah Wilson", 104, "444-987-6543", "sarah.wilson@example.com", "321 Maple St, Springfield", "Female"}
};

Patient patients[MAX_PATIENTS];
int numDoctors = 4;
int numPatients = 0;

void addDoctor() {
    if (numDoctors >= MAX_DOCTORS) {
        printf("\nDoctor list is full. Cannot add more doctors.\n");
        return;
    }

    Doctor newDoctor;
    printf("\nEnter Doctor's Name: ");
    fgets(newDoctor.name, sizeof(newDoctor.name), stdin);
    newDoctor.name[strcspn(newDoctor.name, "\n")] = 0;

    printf("Enter Admin No: ");
    scanf("%d%*c", &newDoctor.adminNo);

    printf("Enter Phone: ");
    fgets(newDoctor.phone, sizeof(newDoctor.phone), stdin);
    newDoctor.phone[strcspn(newDoctor.phone, "\n")] = 0;

    printf("Enter Email: ");
    fgets(newDoctor.email, sizeof(newDoctor.email), stdin);
    newDoctor.email[strcspn(newDoctor.email, "\n")] = 0;

    printf("Enter Address: ");
    fgets(newDoctor.address, sizeof(newDoctor.address), stdin);
    newDoctor.address[strcspn(newDoctor.address, "\n")] = 0;

    printf("Enter Gender: ");
    fgets(newDoctor.gender, sizeof(newDoctor.gender), stdin);
    newDoctor.gender[strcspn(newDoctor.gender, "\n")] = 0;

    doctors[numDoctors++] = newDoctor;
    printf("\nDoctor added successfully.\n");
}

void addPatient() {
    if (numPatients >= MAX_PATIENTS) {
        printf("\nPatient list is full. Cannot add more patients.\n");
        return;
    }

    Patient newPatient;
    printf("\nEnter Patient's Name: ");
    fgets(newPatient.name, sizeof(newPatient.name), stdin);
    newPatient.name[strcspn(newPatient.name, "\n")] = 0;

    printf("Enter Patient ID: ");
    scanf("%d%*c", &newPatient.patientID);
    
    for (int i = 0; i < numPatients; i++) {
        if (patients[i].patientID == newPatient.patientID) {
            printf("\nError: Patient ID already exists. Please enter a unique ID.\n");
            return;
        }
    }

    printf("Enter Phone: ");
    fgets(newPatient.phone, sizeof(newPatient.phone), stdin);
    newPatient.phone[strcspn(newPatient.phone, "\n")] = 0;

    printf("Enter Ailment: ");
    fgets(newPatient.ailment, sizeof(newPatient.ailment), stdin);
    newPatient.ailment[strcspn(newPatient.ailment, "\n")] = 0;

    patients[numPatients++] = newPatient;
    printf("\nPatient added successfully.\n");
}

void doctorDetails() {
    int adminNo;
    printf("\nEnter the Admin No of the doctor to view details: ");
    scanf("%d", &adminNo);

    for (int i = 0; i < numDoctors; i++) {
        if (doctors[i].adminNo == adminNo) {
            printf("\n--- Details of %s ---\n", doctors[i].name);
            printf("Phone: %s\nEmail: %s\nAddress: %s\nGender: %s\n", 
                   doctors[i].phone, doctors[i].email, doctors[i].address, doctors[i].gender);
            return;
        }
    }
    printf("\nNo doctor found with Admin No: %d\n", adminNo);
}

void doctorsInformation() {
    printf("\n--- Information of Doctors ---\n");
    for (int i = 0; i < numDoctors; i++) {
        printf("%d. %s (Admin No: %d)\n", i + 1, doctors[i].name, doctors[i].adminNo);
    }
    doctorDetails();
}

void patientsInformation() {
    printf("\n--- Information of Patients ---\n");
    for (int i = 0; i < numPatients; i++) {
        printf("%d. %s (Patient ID: %d, Phone: %s, Ailment: %s)\n", 
               i + 1, patients[i].name, patients[i].patientID, patients[i].phone, patients[i].ailment);
    }
    if (numPatients == 0) {
        printf("No patients available.\n");
    }
}

void termsAndConditions() {
    printf("\n--- Terms and Conditions ---\n");
    printf("1. Please provide accurate information.\n");
    printf("2. All data is confidential.\n");
    printf("3. Follow hospital rules and regulations.\n");
    printf("4. Payment must be completed before treatment.\n");
}

void healthInsuranceDetails() {
    printf("\n--- Health Insurance Details ---\n");
    printf("1. Insurance Partner: ABC Health\n");
    printf("2. Coverage: Up to $100,000\n");
    printf("3. Contact: 123-456-7890\n");
}

int main() {
    int choice;
    while (1) {
        printf("\n--- Hospital Management Main Page ---\n");
        printf("1. Information of Doctors\n");
        printf("2. Information of Patients\n");
        printf("3. Add Doctor Information\n");
        printf("4. Add Patient Information\n");
        printf("5. Terms and Conditions\n");
        printf("6. Health Insurance Details\n");
        printf("7. Exit\n");
        printf("Enter your choice: ");
        scanf("%d%*c", &choice);

        switch (choice) {
            case 1: doctorsInformation(); break;
            case 2: patientsInformation(); break;
            case 3: addDoctor(); break;
            case 4: addPatient(); break;
            case 5: termsAndConditions(); break;
            case 6: healthInsuranceDetails(); break;
            case 7: printf("\nExiting the program. Thank you!\n"); exit(0);
            default: printf("\nInvalid choice. Please try again.\n");
        }
    }
    return 0;
}
