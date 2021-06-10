# Exercise 8.3.2
## Question
Complete and run the tests to satisfy CACC for the <span style="font-family:Courier">Thermostat</span> class.

### Thermostat class
```Java
import java.io.*;
import java.util.*;

// Programmable Thermostat
public class Thermostat
{
   private int curTemp;          // current temperature reading
   private int thresholdDiff;    // temp difference until we turn heater on
   private int timeSinceLastRun; // time since heater stopped
   private int minLag;           // how long I need to wait
   private boolean override;     // has user overridden the program
   private int overTemp;         // overriding temperature
   private int runTime;          // output of turnHeaterOn - how long to run
   private boolean heaterOn;     // output of turnHeaterOn - whether to run
   private Period period;        // morning, day, evening, or night
   private DayType day;          // week day or weekend day

   // Decide whether to turn the heater on, and for how long.
   public boolean turnHeaterOn (ProgrammedSettings pSet)
   {
      int dTemp = pSet.getSetting(period, day);

      if (((curTemp < dTemp - thresholdDiff) ||
           (override && curTemp < overTemp - thresholdDiff)) &&
           (timeSinceLastRun > minLag))
      {  // Turn on the heater
         // How long? Assume 1 minute per degree (Fahrenheit)
         int timeNeeded = Math.abs(dTemp - curTemp); // abs() added May 2020
         if (override)
            timeNeeded = Math.abs(overTemp - curTemp); // abs() added May 2020
         setRunTime(timeNeeded);
         setHeaterOn(true);
         return(true);
      }
      else
      {
         setHeaterOn(false);
         return(false);
      }
   } // End turnHeaterOn

   public void setCurrentTemp(int temperature)  { curTemp = temperature; }
   public void setThresholdDiff(int delta)      { thresholdDiff = delta; }
   public void setTimeSinceLastRun(int minutes) { timeSinceLastRun = minutes; }
   public void setMinLag(int minutes)           { minLag = minutes; }
   public void setOverride(boolean value)       { override = value; }
   public void setOverTemp(int temperature)     { overTemp = temperature; }

   // for the ProgrammedSettings
   public void setDay(DayType curDay)      { day = curDay; }
   public void setPeriod(Period curPeriod) { period = curPeriod; }

   // outputs from turnHeaterOn
   void    setRunTime(int minutes)    { runTime = minutes; }
   int     getRunTime()               { return runTime; }
   void    setHeaterOn(boolean value) { heaterOn = value; }
   boolean getHeaterOn()              { return heaterOn; }
} // End Thermostat class
```

## Answer

```Java
public class Test_Thermostat
{
  @Test
  public void test_CC()
  {
    Thermostat t = new Thermostat();
    ProgrammedSettings s = new ProgrammedSettings();

    s.setSetting(Period.MORNING, DayType.WEEKDAY, 69);
    t.setPeriod(Period.MORNING);
    t.setDay(DayType.WEEKDAY);

    t.setCurrentTemp(63);
    t.setThresholdDiff(5);

    t.setCurrentTemp(66);
    t.setThresholdDiff(5);

    t.setOverride(true);
    t.setOverride(false);

    t.setOverTemp(72);
    t.setOverTemp(67);

    t.setMinLag(10);
    t.setTimeSinceLastRun(12);

    t.setMinLag(10);
    t.setTimeSinceLastRun(8);

    assertTrue(t.turnHeaterOn(s));
  }
}
```