# Exercise 8.3.1
## Question
Complete and run the tests to satisfy PC for the <span style="font-family:Courier">Thermostat</span> class.
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
There are 4 clauses:  
- a: curTemp < dTemp - thresholdDiff    
- b: Override  
- c: curTemp < overTemp - thresholdDiff  
- d: timeSinceLastRun > minLag  

And 2 predicates:
- p1: ((curTemp < dTemp - thresholdDiff) || (override && curTemp < overTemp - thresholdDiff)) && (timeSinceLastRun > minLag)
- p2: override

### Test_Thermostat class
```Java
import org.junit.Test;
import static org.junit.Assert.*;
import java.io.*;
import java.util.*;
public class Test_Thermostat
{
  @Before
	public void init(){
		Thermostat ts = new Thermostat();
		ProgrammedSettings s = ProgrammedSettings();
	}
	@Test
	public void test_PC_true(){
		s.setSetting(Period.MORNING, DayType.WEEKDAY, 69);
    		ts.setPeriod(Period.MORNING);
    		ts.setDay(DayType.WEEKDAY);
    		//clause a
    		ts.setCurrentTemp(63);
    		ts.setThresholdDiff(5);
    		//clause b
    		ts.setOverride(true);
    		//clause c
	    	ts.setOverTemp(70);
	    	//clause d
    		ts.setMinLag(10);
    		ts.setTimeSinceLastRun(12);
    		assertTrue(ts.turnHeaterOn(s));
	}
	// Test each predicate to false to satisfy PC.
	public void test_PC_false(){
		s.setSetting(Period.MORNING, DayType.WEEKDAY, 69);
    		ts.setPeriod(Period.MORNING);
    		ts.setDay(DayType.WEEKDAY);
    		//clause a: false
    		ts.setCurrentTemp(63);
    		ts.setThresholdDiff(15);
    		//clause b: false
    		ts.setOverride(false);
    		//clause c: false
	    	ts.setOverTemp(60);
	    	//clause d: false
    		ts.setMinLag(15);
    		ts.setTimeSinceLastRun(12);
    		assertFalse(ts.turnHeaterOn(s));
	}
}
```