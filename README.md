// A Simple Java Project: University Accountants Management System
// This program allows users to manage university staff accountants' records.

import java.util.ArrayList;
import java.util.Scanner;

class Accountant {
    private String name;
    private int id;
    private double salary;

    public Accountant(String name, int id, double salary) {
        this.name = name;
        this.id = id;
        this.salary = salary;
    }

    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Salary: $" + salary;
    }
}

class AccountantManager {
    private ArrayList<Accountant> accountants;

    public AccountantManager() {
        this.accountants = new ArrayList<>();
    }

    public void addAccountant(String name, int id, double salary) {
        accountants.add(new Accountant(name, id, salary));
        System.out.println("Accountant \"" + name + "\" added successfully!");
    }

    public void viewAccountants() {
        if (accountants.isEmpty()) {
            System.out.println("No accountants available.");
            return;
        }

        System.out.println("\nList of Accountants:");
        for (Accountant accountant : accountants) {
            System.out.println(accountant);
        }
    }

    public void updateSalary(int id, double newSalary) {
        for (Accountant accountant : accountants) {
            if (accountant.getId() == id) {
                accountant.setSalary(newSalary);
                System.out.println("Updated salary for Accountant ID " + id + ".");
                return;
            }
        }
        System.out.println("Accountant with ID " + id + " not found.");
    }

    public void deleteAccountant(int id) {
        for (int i = 0; i < accountants.size(); i++) {
            if (accountants.get(i).getId() == id) {
                System.out.println("Deleted Accountant: " + accountants.get(i));
                accountants.remove(i);
                return;
            }
        }
        System.out.println("Accountant with ID " + id + " not found.");
    }
}

public class Main {
    public static void main(String[] args) {
        AccountantManager manager = new AccountantManager();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nUniversity Accountants Management System");
            System.out.println("1. Add Accountant");
            System.out.println("2. View Accountants");
            System.out.println("3. Update Accountant Salary");
            System.out.println("4. Delete Accountant");
            System.out.println("5. Exit");

            System.out.print("Enter your choice: ");
            String choice = scanner.nextLine();

            switch (choice) {
                case "1":
                    System.out.print("Enter Accountant Name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter Accountant ID: ");
                    int id;
                    try {
                        id = Integer.parseInt(scanner.nextLine());
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid ID. Please enter a number.");
                        break;
                    }
                    System.out.print("Enter Accountant Salary: ");
                    double salary;
                    try {
                        salary = Double.parseDouble(scanner.nextLine());
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid salary. Please enter a valid amount.");
                        break;
                    }
                    manager.addAccountant(name, id, salary);
                    break;
                case "2":
                    manager.viewAccountants();
                    break;
                case "3":
                    System.out.print("Enter Accountant ID to update salary: ");
                    try {
                        id = Integer.parseInt(scanner.nextLine());
                        System.out.print("Enter new salary: ");
                        salary = Double.parseDouble(scanner.nextLine());
                        manager.updateSalary(id, salary);
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid input. Please enter valid numbers.");
                    }
                    break;
                case "4":
                    System.out.print("Enter Accountant ID to delete: ");
                    try {
                        id = Integer.parseInt(scanner.nextLine());
                        manager.deleteAccountant(id);
                    } catch (NumberFormatException e) {
                        System.out.println("Invalid ID. Please enter a number.");
                    }
                    break;
                case "5":
                    System.out.println("Exiting University Accountants Management System. Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
