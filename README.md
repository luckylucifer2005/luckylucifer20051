# luckylucifer20051
import java.util.Random;
import java.util.Scanner;

public class NumberGame {
    
    private static final int Max_Attempts = 7;
    private static final int Lower_Bound = 1;
    private static final int Upper_Bound = 100;
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Random Rd = new Random();
        int TRounds = 0;
        int TWins = 0;
        
        boolean playAgain = true;
        while (playAgain) {
            int NumToGuess = GenerateRanNum(Rd, Lower_Bound, Upper_Bound);
            int AttemptsLeft = Max_Attempts;
            boolean GuessedCorrectly = false;
            
            System.out.println("A new number between " + Lower_Bound + " and " + Upper_Bound + " has been generated.");
            
            while (AttemptsLeft > 0 && !GuessedCorrectly) {
                System.out.println("You have " + AttemptsLeft + " attempts left. Enter your guess:");
                int UserGuess = getUserGuess(sc);
                
                if (UserGuess == NumToGuess) {
                    System.out.println("Congratulations! You've guessed the correct number!");
                    GuessedCorrectly = true;
                } else if (UserGuess < NumToGuess) {
                    System.out.println("Too low! Try again.");
                } else {
                    System.out.println("Too high! Try again.");
                }
                
                AttemptsLeft--;
            }
            
            if (!GuessedCorrectly) {
                System.out.println("Sorry, you've run out of attempts. The correct number was: " + NumToGuess);
            } else {
                TWins++;
            }
            
            TRounds++;
            
            System.out.println("Your current score: " + TWins + " Wins out of " + TRounds + " Rounds.");
            System.out.println("Would you like to play another round? (yes/no)");
            String response = sc.next().toLowerCase();
            if (!response.equals("yes")) {
                playAgain = false;
            }
        }
        
        System.out.println("Thanks for playing! Final score: " + TWins + " Wins out of " + TRounds + " Rounds.");
        sc.close();
    }
    
    private static int GenerateRanNum(Random Rd, int lowerBound, int upperBound) {
        return Rd.nextInt(upperBound - lowerBound + 1) + lowerBound;
    }
    
    private static int getUserGuess(Scanner sc) {
        while (!sc.hasNextInt()) {
            System.out.println("Invalid input. Please enter a number.");
            sc.next(); 
        }
        return sc.nextInt();
    }
}
