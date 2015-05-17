# Repository-7
It would be perfectly reasonable for the Time2 class of Fig. 8.5 to represent the time internally as the number of seconds since midnight rather than the three integer values hour, minute and second. Clients could use the same public methods and get the same results. Modify the Time2 class of Fig. 8.5 to implement the Time2 as the number of seconds since midnight and show that no change is visible to the clients of the class.


public class Time2
{
   private int ssm;
   public Time2()
   {
      this(0, 0, 0);
   } 
   public Time2(int hour) 
   { 
      this(hour, 0, 0);
   } 
   public Time2(int hour, int minute) 
   { 
      this(hour, minute, 0);
   } 
   public Time2(int hour, int minute, int second) 
   { 
      if (hour < 0 || hour >= 24)
         throw new IllegalArgumentException("hour must be 0-23");

      if (minute < 0 || minute >= 60)
         throw new IllegalArgumentException("minute must be 0-59");

      if (second < 0 || second >= 60)
         throw new IllegalArgumentException("second must be 0-59");

      this.ssm = (hour*3600)+(minute*60)+second; 
   } 
   public Time2(Time2 time)
   {
      this(time.getHour(), time.getMinute(), time.getSecond());
   } 
   public void setTime(int hour, int minute, int second)
   {
      if (hour < 0 || hour >= 24)
         throw new IllegalArgumentException("hour must be 0-23");

      if (minute < 0 || minute >= 60)
         throw new IllegalArgumentException("minute must be 0-59");

      if (second < 0 || second >= 60)
         throw new IllegalArgumentException("second must be 0-59");

      this.ssm = (hour*3600)+(minute*60)+second;
   } 
   public void setHour(int hour) 
   { 
      if (hour < 0 || hour >= 24)
         throw new IllegalArgumentException("hour must be 0-23");
      else
      this.ssm=(hour*3600)+(getMinute()*60)+getSecond();
   } 
   public void setMinute(int minute) 
   { 
      if (minute < 0 || minute >= 60)
         throw new IllegalArgumentException("minute must be 0-59");
      else
      this.ssm = (getHour()*3600)+(minute*60)+getSecond(); 
   } 
   public void setSecond(int second) 
   { 
      if (second < 0 || second >= 60)
         throw new IllegalArgumentException("second must be 0-59");
      else
    	  this.ssm=(getHour()*3600)+(getMinute()*60)+ second; 
      
   }

        
   public int getHour() 
   { 
      return (ssm/3600); 
   } 
   public int getMinute() 
   { 
      return (( ssm%3600)/60); 
   } 
   public int getSecond() 
   { 
      return (ssm%60); 
   } 
   public String toUniversalString()
   {
      return String.format("%02d:%02d:%02d", getHour(), getMinute(), getSecond());
   } 
   public String toString()
   {
      return String.format("%d:%02d:%02d %s", 
         ((getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12),
         getMinute(), getSecond(), (getHour() < 12 ? "AM" : "PM"));
   } 
}
// Test Program


public class Time2Test 
{
   public static void main(String[] args)
   {
      Time2 t1 = new Time2(); // 00:00:00
      Time2 t2 = new Time2(2); // 02:00:00
      Time2 t3 = new Time2(21, 34); // 21:34:00
      Time2 t4 = new Time2(12, 25, 42); // 12:25:42
      Time2 t5 = new Time2(t4); // 12:25:42

      System.out.println("Constructed with:");
      displayTime("t1: all default arguments", t1);
      displayTime("t2: hour specified; default minute and second", t2);
      displayTime("t3: hour and minute specified; default second", t3);
      displayTime("t4: hour, minute and second specified", t4);
      displayTime("t5: Time2 object t4 specified", t5);

      // attempt to initialize t6 with invalid values
      try
      {
         Time2 t6 = new Time2(27, 74, 99); // invalid values
      } 
      catch (IllegalArgumentException e)
      {
         System.out.printf("%nException while initializing t6: %s%n",
            e.getMessage());
      } 
   } 

   // displays a Time2 object in 24-hour and 12-hour formats
   private static void displayTime(String header, Time2 t)
   {
      System.out.printf("%s%n   %s%n   %s%n",
         header, t.toUniversalString(), t.toString());
   } 
} // end class Time2Test
