# Problem: Mini-Max Sum

Given five positive integers, find the minimum and maximum values that can be calculated by summing exactly four of the five integers. Then print the respective minimum and maximum values as a single line of two space-separated long integers.

For example,  `arr = [1, 3, 5, 7, 9]`. Our minimum sum is `1 + 3 + 5 + 7 = 16` and our maximum sum is `3 + 5 + 7 + 9 = 24` . 
We would print `16 24`
### Sample Input:  `1 2 3 4 5`
### Sample output: `10 14`

# Analyze
### Normal
To compute 2 larger number in school mathematics:
	1) Reverse 2 number.
	2) Sum each digits together (carry).
	3) Reverse the result string.
### Optimize
# Solution

    import java.io.*;
    import java.math.*;
    import java.security.*;
    import java.text.*;
    import java.util.*;
    import java.util.concurrent.*;
    import java.util.regex.*;
    
    public class Solution {

    static String sumLargeNum(String firstNum, String secondNum){
        String result = "";

        //Before proceeding further, make sure length of secondNum is larger.
        if (firstNum.length() > secondNum.length()){
            String tmp = firstNum;
            firstNum = secondNum;
            secondNum = tmp;
        }

        // Calculate length both of String
        int lenNum1 = firstNum.length();
        int lenNum2 = secondNum.length();

        //Reverse both of String
        firstNum = new StringBuilder(firstNum).reverse().toString();
        secondNum = new StringBuilder(secondNum).reverse().toString();

        int carry = 0;
        for (int i = 0; i < lenNum1 ; i++){
            // Do school mathematics, compute sum of current digits and carry
            int sum = ((int)(firstNum.charAt(i) - '0') + (int)(secondNum.charAt(i) - '0') + carry);
            result += (char)(sum % 10 + '0');
            // Calculate carry for next step
            carry = sum / 10;
        }

        //Adding remaining digits of larger number
        for (int i = lenNum1; i < lenNum2; i++){
            int sum = ((int)(secondNum.charAt(i) - '0') + carry);
            result += (char)(sum%10 + '0');
            carry = sum / 10;
        }

        //Adding remaining carry
        if (carry > 0){
            result += (char)(carry + '0');
        }

        //Reverse resultant String
        result = new StringBuilder(result).reverse().toString();

        return result;
    }

    // Complete the miniMaxSum function below.
    static void miniMaxSum(int[] arr) {
        Arrays.sort(arr);
        String[] arrString = Arrays.stream(arr)
                                    .mapToObj(String::valueOf)
                                    .toArray(String[]::new);
        String min = "0";
        String max = "0";
        for (int i = 0; i < arrString.length; i++){
            if (i != (arr.length - 1)){
                min = sumLargeNum(min, arrString[i]);
            }
        }

        for (int i = 0; i < arr.length; i++){
            if (i != 0){
                max = sumLargeNum(max, arrString[i]);
            }
        }
        System.out.print(min + " " + max + "\n");
    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int[] arr = new int[5];

        String[] arrItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < 5; i++) {
            int arrItem = Integer.parseInt(arrItems[i]);
            arr[i] = arrItem;
        }

        miniMaxSum(arr);

        scanner.close();
    }
}
