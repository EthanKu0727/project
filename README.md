# project
import java.util.ArrayList;
import java.util.Scanner;

public class Main {

    // Method to check if the input is an integer
    public static boolean checkInt(String x) {
        try {
            Integer.parseInt(x);
        } catch (NumberFormatException e) {
            return false;
        }
        return true;
    }

    // Main method to run the budget planner
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Ask for the username
        System.out.print("Type your First Name: ");
        String firstName = scanner.nextLine();
        System.out.print("Type your Last Name: ");
        String lastName = scanner.nextLine();

        String name = firstName + " " + lastName;
        System.out.println("Welcome to the Ultimate Budget Planner " + name.toUpperCase());

        // Ask for the user's budget
        System.out.print("What's your budget right now? ");
        String budgetInput = scanner.nextLine();
        while (!checkInt(budgetInput)) {
            System.out.println("Please input a valid value! (numbers)");
            System.out.print("What's your budget right now? ");
            budgetInput = scanner.nextLine();
        }
        int budget = Integer.parseInt(budgetInput);

        boolean stillWantToBuy = true;
        int total = 0;
        ArrayList<String> pList = new ArrayList<>();

        // Loop for item input and budget calculation
        while (stillWantToBuy) {
            System.out.print("What item do you want to buy? ");
            String pName = scanner.nextLine();
            pList.add(pName);

            System.out.print("How much is it? ");
            String pPriceInput = scanner.nextLine();
            while (!checkInt(pPriceInput)) {
                System.out.println("Please input an integer");
                System.out.print("How much is it? ");
                pPriceInput = scanner.nextLine();
            }
            int pPrice = Integer.parseInt(pPriceInput);
            total += pPrice;

            // Loop for checking additional items
            boolean validOption = false;
            while (!validOption) {
                System.out.print("Do you still have other items you want to buy? (Yes/No) ");
                String option = scanner.nextLine().trim().toUpperCase();
                if (option.equals("NO")) {
                    if (pList.size() <= 1) {
                        System.out.println("Sorry, you need to input at least 2 items!");
                        break;
                    }
                    stillWantToBuy = false;
                    validOption = true;
                    if (total < budget) {
                        System.out.println("Here is the summary:");
                        int count = 1;
                        for (String item : pList) {
                            System.out.println("Item #" + count + ": " + item);
                            count++;
                        }
                        System.out.println("Total Expense: " + total);
                        System.out.println("Remaining budget: " + (budget - total));
                    } else {
                        System.out.println("Sorry, you don't have enough budget");
                    }
                } else if (option.equals("YES")) {
                    validOption = true;
                } else {
                    System.out.println("Please enter a valid option (Yes/No)");
                }
            }
        }
        scanner.close();
    }
}

