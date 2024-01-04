import java.util.Scanner;

public class StringsClass {

    static Scanner in;
    static String sentence = "The quick brown fox jumps over the lazy dog";
    static String operationEntered = ""; //holds the word FACTORIAL with Number.
    static String operation = ""; //holds the extracted word FACTORIAL.
    static String numberValue = ""; //holds the extracted Number.
    static int number; //holds the converted Number.
    static boolean isFactorial=false; //used to check if the extracted word is FACTORIAL.
    static boolean isRepeat=false; //used to hold try again response.
    static boolean isValid=false; //used for checking if conversion is valid.
    static int length; //holds the length size of the operationEntered.

    public static void main(String[] args) {

        do{
            enterOperation();

            startFactorial();

            checkRepeat();
        }while(isRepeat);


    }

    static void startFactorial(){
        if(isValid){
            if(operation.equals("FACTORIAL")){
                if(number<1){
                    System.out.println("Invalid Numbers.");
                }else{
                    runFactorial();
                }
            }else{
                System.out.println("Invalid Operation.");
            }
        }else{
            System.out.println("Invalid Conversion.");
        }

    }

    static void checkRepeat(){
        char select;
        System.out.print("Do you want to try again? [Y]Yes [N]No: " );
        select = in.next().charAt(0);
        switch (select){
            case 'Y':
            case 'y':
                isRepeat = true;
                break;
            default:
                isRepeat = false;
        }
    }

    static void runFactorial(){
        int factorial=1;
        System.out.print(number+"! = ");
        for(int x=1; x<=number; x++){
            if(x<number){
                System.out.print(x+ " x ");
            }else{
                System.out.print(x);
            }
            factorial = factorial * x;
        }

        System.out.println("\nThe factorial of "+number+" is: "+ factorial);
    }

    static void enterOperation(){
        in = new Scanner(System.in);

        System.out.print("Enter Operation: ");
        operationEntered = in.nextLine();

        extractOperation();
    }

    static void extractOperation(){
        char currentChar;
        for(int x=0; x<operationEntered.length(); x++){
            currentChar = operationEntered.toUpperCase().charAt(x);
            if(currentChar == ' '){
                operation = operationEntered.substring(0, x).toUpperCase();
                if(operation.equals("FACTORIAL")){
                    isFactorial = true;
                    break;
                }
            }
        }

        if(!operation.equals(" ")){ //check if operation is not blank.
                    extractNumberString();
            //        extractNumberChar();
        }

    }

    static void extractNumberString(){
        char currentChar; //used in the loop to hold the character values.
        length = operationEntered.length();
        for(int x=length-1; x>0; x--){
            currentChar = operationEntered.charAt(x);
            if(currentChar == ' '){
                isValid = true; //valid conversion
                numberValue = operationEntered.substring(x+1, length); //get the substring after the space
                number = Integer.parseInt(numberValue); // convert of String to Integer
                break;
            }
        }
    }

    static void extractNumberChar(){
        char currentChar;
        length = operationEntered.length();
        for(int x=length-1; x>0; x--){
            currentChar = operationEntered.charAt(x);
            if(currentChar == ' '){ //check if character read is space
                if(x+1 < length){
                    numberValue = operationEntered.substring(x+1, length); //get the substring after the space
                    if(numberValue.length()<2) { //will only execute the statement if less than 2 character (char).
                        isValid = true; //valid conversion
                        number = (operationEntered.charAt(x + 1)) - 48; //get the character after space and perform implicit casting char(ASCII) to int
                    }
                    else{
                        isValid = false; //invalid conversion
                    }
                }
                break;
            }
        }
    }

    static void startPart1(){
        for(int y=1; y<10; y++){
            for(int x=1; x<y; x++){
                for(int i=1; i<x; i++){
                    System.out.print("*");
                }
            }
            System.out.println();
        }
    }
    static void Problem1(){

        int count = 0; //variable that holds the number of characters

            for (int i = 0;i < sentence.length(); i++){

            if (sentence.charAt(i) == 'u') {
                count++;
            }

        }

        System.out.println("The letter 'o' appears "+ count + " in the given sentence");
    }
    static void Problem2(){
        String str1 = "Class";
        String str2 = "        class ";

        boolean areEqualIgnoreCaseAndTrimmed=str1.trim().equalsIgnoreCase(str2.trim());
        System.out.println (areEqualIgnoreCaseAndTrimmed);
    }
    static void Problem3() {
        String modified = sentence.replace(' ','%');
        System.out.println(modified);

    }

}
