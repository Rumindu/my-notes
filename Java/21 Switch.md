# Switch
``` java
public class Main {
    public static void main(String[] args) {
        String role = "admin";
        switch (role) {
            //no need to use curly braces in case block,
            // even for multiple lines
            case "admin":
                int x=4;
                System.out.println("You're an admin");
                System.out.println(x);
                //once the case block is executed,
                // it will jump out from switch block because of break statement
                break;
            case "moderator":
                System.out.println("You're a moderator");
                break;
            // no need to use break statement in default block
            default:
                System.out.println("You're a guest");
        }
    }
}
 ``` 