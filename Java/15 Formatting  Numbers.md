# Formatting numbers

- We use `NumberFormat` class for formatting. which import by `java.text` package.
- But this class is abstract. we couldn't use new key word for instantiate. 

## Currency formatting

- Long way
  ``` java 
  import java.text.NumberFormat;

  public class Main {
      public static void main(String[] args) {
          // creating currency object, which type is NumberFormat
          NumberFormat currency = NumberFormat.getCurrencyInstance();
          String result=currency.format(1234567.891);
          System.out.println(result);//$1,234,567.89
      }
  }
  ```

- Short way (method chaining way)
  ``` java 
  import java.text.NumberFormat;

  public class Main {
      public static void main(String[] args) {
          // creating currency object, which type is NumberFormat
          String result = NumberFormat.getCurrencyInstance().format(1234567.891);
          System.out.println(result);//$1,234,567.89
      }
  }

  ```
## Percentage

- long way
``` java 
import java.text.NumberFormat;

public class Main {
    public static void main(String[] args) {
        NumberFormat precent = NumberFormat.getPercentInstance();
        String result=precent.format(0.1);
        System.out.println(result);//10%
    }
}
```

- method chaining
``` java 
import java.text.NumberFormat;

public class Main {
    public static void main(String[] args) {
        String result=NumberFormat.getPercentInstance().format(0.1);
        System.out.println(result);//10%
    }
}

```