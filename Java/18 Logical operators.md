# Logical Operators
## &&
- This is Boolean AND operator.
``` java 
public class Main {
    public static void main(String[] args) {
      int temperature = 22;
      //java is evaluating this expression from left to right.
      // if the first part is false, it will not evaluate the second part.
      boolean isWarm = temperature > 20 && temperature < 30;
      System.out.println(isWarm);//true
    }
}
```

## || 
- This is Boolean OR operator.
``` java 
public class Main {
    public static void main(String[] args) {
        boolean hasHighIncome = true;
        boolean hasGoodCredit = true;
        //java is evaluating this expression from left to right.
        //if the first operand is true, it will not evaluate the second operand.
        //if the first operand is false, it will evaluate the second operand.
        boolean isEligible = hasHighIncome || hasGoodCredit;
        System.out.println(isEligible);//true
    }
}
```

## !
- This is Boolean NOT operator.
``` java 
public class Main {
    public static void main(String[] args) {
        boolean hasHighIncome = true;
        boolean hasGoodCredit = true;
        boolean hasCriminalRecord = false;
        boolean isEligible = (hasHighIncome || hasGoodCredit) && !hasCriminalRecord;
        // !hasCriminalRecord = true
        System.out.println(isEligible);//true
    }
}
```
