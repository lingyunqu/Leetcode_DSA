```java
public class Loopy {
   public static void main (String[] args) {
     int x = 1;
     System.out.println(“Before the Loop”);
     while (x < 4) {
       System.out.println(“In the loop”);
       System.out.println(“Value of x is ” + x);
x = x + 1; }
     System.out.println(“This is after the loop”);
   }
}
```

println在后面插入换行，printn在同一行打印

```java
public class BeerSong {
       public static void main (String[] args) {
         int beerNum = 99;
         String word = "bottles";
         while (beerNum > 0) {
if (beerNum == 1) {
word = “bottle”; //      
}
            System.out.println(beerNum + "" + word + " of beer on the wall");
            System.out.println(beerNum + "" + word + " of beer.");
            System.out.println("Take one down.");
            System.out.println("Pass it around.");
            beerNum = beerNum - 1;
            if (beerNum > 0) {
               System.out.println(beerNum + " " + word + " of beer on the wall");
            } else {
               System.out.println("No more bottles of beer on the wall");
         }//else  结束
      } //while    结束
   } //main    结束
} //class  结束
```
