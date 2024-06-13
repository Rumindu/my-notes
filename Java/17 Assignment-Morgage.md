``` java 
import java.text.NumberFormat;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        //to prevent putting magic values in the code, we can use constants
        final byte MONTHS_IN_YEAR= 12;
        final byte PERCENT= 100;
        Scanner scanner1= new Scanner(System.in);
        System.out.print("Principal: ");
        float principal= scanner1.nextFloat();
        System.out.print("Annual Interest Rate: ");
        float annualInterestRate= scanner1.nextFloat();
        System.out.print("Period (Years): ");
        int period= scanner1.nextInt();
        float monthlyInterestRate= annualInterestRate/MONTHS_IN_YEAR/PERCENT;
        int numberOfPayments= period*MONTHS_IN_YEAR;
        double mortgage= principal*
                monthlyInterestRate*Math.pow(1+monthlyInterestRate, numberOfPayments)
                /(Math.pow(1+monthlyInterestRate, numberOfPayments)-1);
        String mortgageFormatted= NumberFormat.getCurrencyInstance().format(mortgage);
        System.out.println("Mortgage: "+ mortgageFormatted);
    }
}
```