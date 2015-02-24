# Converting-Plain-Text-Documents-to-HTML
public class TextFormatter
{
    private String line; 

    public TextFormatter (String lineToFormat)
    {	
        line = lineToFormat;	
    }


    /**
     * Finds the first single instance of str in line,
     * starting at the position start
     * @param str the string of length 1 to find.
     * Guaranteed to be length 1.
     * @param start the position to start searching.
     * Guaranteed to be in the string line.
     * @return the index of the first single instance of
     * str if the string is found or -1 if it is not found.
     */
    public int findString (String str, int start)
    {	
        
        int psn = line.indexOf(str, start);
      
           
            while(psn >= 0)
            {
                String before = " ";
                String after = " ";
                                
                    if(psn != 0)
                      before = line.substring(psn-1, psn);
                
                    
                    if(psn != line.length()-1)
                      after = line.substring(psn + 1, psn +2);
                     
                    if(before.equals(str) || after.equals(str)) 
                      psn = line.indexOf(str, psn + 1);
                
                    else
                      return psn;
                                   
             }
               return psn; 
        
    }
    
    public int countStrings(String str)
    {
        int n;
        int t = 0;
        int p = 0;
        n = findString(str, p);
        for(int i = 0; i < line.length(); i++)
        {
          if (n > 0)
          {
           t++;
           p =n;
           n = findString(str, p+1);
          }
         
                  
        }
        return t;
    }
    
    
        public String convertItalics()
    {
        int n;
        int t = 0;
        int p = 0;
        n = findString("_", p);
        int len = line.length();
        for(int i = 0; i < line.length(); i++)
        {
          if (n > 0)
          {
           t++;
           p =n;
           n = findString("_", p+1);
          } 
        }
          String s = " ";
          p = 0;
          if(t % 2 == 0)
          {
                        
            for(int i = 0; i < line.length(); i++)
            {
                n = findString("_",p);
                if( n > 0 && p >= 0)
                {
                    n = findString("_",p);
                    if(n>p)
                      s = s + line.substring(p,n) + "<I>";
                    
                    p = n + 1;
                    n = findString("_", p+1);
                    if( n > 0)
                    {                    
                    
                    s = s + line.substring((p), n) + "</I>";
                    }
                    
                    else
                    {
                      s = s + line.substring(p, line.length());
                    }
                    
                    
                    p = n  ;
                }
            }
                                     
          }
          
          else
          {
              return line;
          }
            
        return s;
    }

}

public class Driver 
{
    public static void main(String []args)
    {
        String n;
        String m;
        String s;
        m = "This is _very_ good.";
        n = "aabaccba";
        TextFormatter t = new TextFormatter(m);
        int c = t.findString("_", 13);
        s = t.convertItalics();
        int l = t.countStrings("a");
    
        System.out.println(s);
        
       
    }
}
