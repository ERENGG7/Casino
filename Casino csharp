using System;
using System.Collections;
using System.Collections.Generic;



namespace IEnumerations_1._0
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.OutputEncoding = System.Text.Encoding.UTF8;
            int balance = 100;
            int bet;
            int totalPriseWin = 0;
            Random rand = new Random();
            List<string> emotikons = new List<string>() { "🥭", "🎲", "🍇", "🍋", "🍉", "🍒", "🎰" };

            while (true)
            {

                Console.Clear();
                Console.WriteLine($"Your balance: {balance}");
                Console.WriteLine("Enter number bigger tha your balance to quit");
                Console.Write("Enter Bet: ");
                try
                {
                    bet = int.Parse(Console.ReadLine());

                }
                catch (FormatException)
                {
                    Console.WriteLine("Invalid choise");
                    Console.ReadKey();
                    continue;
                }
                if (bet <= 0)
                {
                    Console.WriteLine("Invalid bet!");
                    Console.ReadKey();
                    continue;
                }
                else if (bet > balance)
                {
                    Console.WriteLine("Not Enough bet!");
                    Console.ReadKey();
                    break;
                }

                //Creating random for emotikons
                int index1 = rand.Next(emotikons.Count);
                int index2 = rand.Next(emotikons.Count);
                int index3 = rand.Next(emotikons.Count);

                string a = emotikons[index1];
                string b = emotikons[index2];
                string c = emotikons[index3];

                Console.WriteLine($"|{a}|{b}|{c}|");

                if (a == "🎰" && b == "🎰" && c == "🎰")
                {
                    Console.WriteLine("JACKPOT");
                    balance += bet * 100;
                    totalPriseWin += bet * 100;
                    Console.ReadKey();
                    continue;
                }
                else if (a == b && b == c)
                {
                    Console.WriteLine("😎BIG PRISE😎" + bet * 5);
                    balance += bet * 5;
                    totalPriseWin += bet * 5;
                    Console.ReadKey();
                }
                else if (a == b || b == c || a == c)
                {
                    Console.WriteLine("WIN PRISE: " + bet * 2);
                    balance += bet * 2;
                    totalPriseWin += bet * 2;
                    Console.ReadKey();
                }
                else
                {
                    Console.WriteLine("Try Again 😓");
                    balance -= bet;
                    totalPriseWin -= bet;
                    Console.ReadKey();
                }


            }
            if (totalPriseWin < 0)
            {
                totalPriseWin = 0;
            }
            Console.WriteLine($"Total win: {totalPriseWin} BGN");

        }
    }
}
