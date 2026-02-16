using System;

// Base Class
abstract class WaterFilter
{
    private string filterID;
    private int usageCount;

    public string FilterID
    {
        get { return filterID; }
        set { filterID = value; }
    }

    public int UsageCount
    {
        get { return usageCount; }
        set
        {
            if (value < 0) throw new ArgumentException("Usage count cannot be negative.");
            usageCount = value;
        }
    }

    public WaterFilter(string id, int usage)
    {
        FilterID = id;
        UsageCount = usage;
    }

    public abstract void ProcessWater();

    public double CalculateEfficiency(double waterProcessed)
    {
        try
        {
            return waterProcessed / UsageCount; // may throw DivideByZeroException
        }
        catch (DivideByZeroException)
        {
            Console.WriteLine("Cannot calculate efficiency: no water processed yet.");
            return 0;
        }
    }
}

// Sub-Class: CarbonFilter
class CarbonFilter : WaterFilter
{
    public int DebrisRemoved { get; set; }

    public CarbonFilter(string id, int usage, int debris) : base(id, usage)
    {
        DebrisRemoved = debris;
    }

    public override void ProcessWater()
    {
        Console.WriteLine($"Carbon Filter {FilterID} removed {DebrisRemoved} units of debris.");
        UsageCount++;
    }
}

// Sub-Class: ChemicalFilter
class ChemicalFilter : WaterFilter
{
    public double ChemicalLevel { get; set; }

    public ChemicalFilter(string id, int usage, double chemical) : base(id, usage)
    {
        if (chemical < 0) throw new ArgumentException("Chemical level cannot be negative.");
        ChemicalLevel = chemical;
    }

    public override void ProcessWater()
    {
        Console.WriteLine($"Chemical Filter {FilterID} processed water at chemical level {ChemicalLevel}.");
        UsageCount++;
    }
}

// Main Program
class Program
{
    static void Main()
    {
        try
        {
            CarbonFilter carbon = new CarbonFilter("CF01", 0, 15);
            ChemicalFilter chemical = new ChemicalFilter("CH01", 0, 7.5);

            carbon.ProcessWater();
            chemical.ProcessWater();

            Console.WriteLine($"Carbon Filter Efficiency: {carbon.CalculateEfficiency(100):F2}");
            Console.WriteLine($"Chemical Filter Efficiency: {chemical.CalculateEfficiency(80):F2}");
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine($"Input Error: {ex.Message}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Unexpected Error: {ex.Message}");
        }
        finally
        {
            Console.WriteLine("System Shutdown");
        }
    }
}
