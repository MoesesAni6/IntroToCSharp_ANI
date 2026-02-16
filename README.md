

using System;

class Program
{
    static void Main()
    {
        // -----------------------------
        // Task 1: Driver Profile & Distance Validation
        // -----------------------------
        Console.Write("Enter Driver's Full Name: ");
        string driverName = Console.ReadLine(); // string type for names

        Console.Write("Enter Weekly Fuel Budget: ");
        decimal weeklyBudget = decimal.Parse(Console.ReadLine()); // decimal for currency precision

        // Validate distance input using while loop
        double totalDistance;
        do
        {
            Console.Write("Enter Total Distance Traveled this week (1.0 - 5000.0 km): ");
            totalDistance = double.Parse(Console.ReadLine()); // double for distance
            if (totalDistance < 1.0 || totalDistance > 5000.0)
            {
                Console.WriteLine("Error: Distance must be between 1.0 and 5000.0 km.");
            }
        } while (totalDistance < 1.0 || totalDistance > 5000.0);

        // -----------------------------
        // Task 2: Fuel Expense Tracking
        // -----------------------------
        decimal[] fuelExpenses = new decimal[5]; // 1D array for 5 days
        decimal totalFuelSpent = 0;

        for (int i = 0; i < 5; i++)
        {
            Console.Write($"Enter fuel expense for Day {i + 1}: "); // (i+1) for readable day numbers
            fuelExpenses[i] = decimal.Parse(Console.ReadLine());
            totalFuelSpent += fuelExpenses[i];
        }

        decimal avgDailyFuel = totalFuelSpent / 5;

        // -----------------------------
        // Task 3: Performance Analysis
        // -----------------------------
        double efficiency = totalDistance / (double)totalFuelSpent; // convert decimal to double for calculation
        string efficiencyRating;

        if (efficiency > 15)
        {
            efficiencyRating = "High Efficiency";
        }
        else if (efficiency >= 10)
        {
            efficiencyRating = "Standard Efficiency";
        }
        else
        {
            efficiencyRating = "Low Efficiency / Maintenance Required";
        }

        // Budget Status
        bool underBudget = totalFuelSpent <= weeklyBudget;

        // -----------------------------
        // Task 4: Audit Report
        // -----------------------------
        Console.WriteLine("\n--- AUDIT REPORT ---");
        Console.WriteLine($"Driver Name: {driverName}");
        Console.WriteLine("Fuel Expenses (5 days):");

        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($" Day {i + 1}: {fuelExpenses[i]:C}"); // :C formats as currency
        }

        Console.WriteLine($"Total Fuel Spent: {totalFuelSpent:C}");
        Console.WriteLine($"Average Daily Fuel Expense: {avgDailyFuel:C}");
        Console.WriteLine($"Efficiency Rating: {efficiencyRating}");
        Console.WriteLine($"Stayed Under Budget: {underBudget}");
    }
}
