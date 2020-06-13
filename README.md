# rememberGame

        static int PickCard()
        {
            int choise;
            while (int.TryParse(Console.ReadLine(), out choise) == false || choise < 0 || choise > 16) ;
            return choise;

        }


        private static void GenerateRandomMatrix(int[,] matrix)
        {
           
            bool[] booleani = new bool[8];
           
            bool[]  values = new bool[16];

           
          
            int number = 0;
            int value1 = 0;
            int value2 = 0;
            int counter = 0;


            do { 
            Random random_generator = new Random(); // chinese --




                number = random_generator.Next(1, 9);

                value1 = random_generator.Next(1, 17);


                value2 = random_generator.Next(1, 17);


                if (value1 != value2)
                {
                    if (!values[value1-1] && !values [value2 - 1 ] && !booleani[number-1])
                    {
                        values[value1 - 1] = true;

                        values[value2 - 1] = true;

                        booleani[number - 1] = true;

                        matrix[((value1 - 1) / 4), ((value1 - 1) % 4)] = number;

                        matrix[((value2 - 1) / 4), ((value2 - 1) % 4)] = number;

                        counter++;
                      }
                }
               
            } while (counter != 8);
            /*   for (int i = 0; i <= 7; i++)
               {
                   if (boolarr[i] == true)
                   {
                        counter++;
                   }

               }*/




        }

   
        static void PrintMatrix(int[,] matrix)
        {
            // print the matrix
            Console.WriteLine("Matrix:");
            for (int i = 0; i < matrix.GetLength(0); i++)
            {
                for (int j = 0; j < matrix.GetLength(1); j++)
                {
                    Console.Write($" {matrix[i, j]} ");
                }
                Console.WriteLine();
            }
        }
        static void Main(string[] args)
        {
            int player1 = 0;

            int player2 = 0;

            int choise = 0;

            int card = 0;

            int card2 = 0;

            int card3 = 0;

            int card4 = 0;


            int[,] matrix = new int[4, 4];

           
            GenerateRandomMatrix(matrix);
           

            PrintMatrix(matrix);
            do
            {
                do
                {
                    if (player1 + player2 == 8)
                        break;
                    Console.WriteLine("player1 turn");
                    do
                    {



                        Console.WriteLine("chose a card between 1-16");

                        card = PickCard();
                        card2 = PickCard();
                        //card3 = PickCard();
                        //card4 = PickCard();
                        if (matrix[(card - 1) / 4, (card - 1) % 4] == 0 || matrix[(card2 - 1) / 4, (card2 - 1) % 4] == 0)
                        {
                            Console.WriteLine("The cards you selected are already found");
                        }

                    } while (matrix[(card - 1) / 4, (card - 1) % 4] == 0 || matrix[(card2 - 1) / 4, (card2 - 1) % 4] == 0);
                    
                    if (matrix[(card - 1) / 4, (card - 1) % 4] == matrix[(card2 - 1) / 4, (card2 - 1) % 4])
                    {
                        player1++;

                        Console.WriteLine("Your answer is right You have another turn");

                        matrix [(card - 1) / 4 , (card - 1) % 4 ]  = 0;

                        matrix[(card2 - 1) / 4, (card2 - 1) % 4] = 0;




                    }

                    else
                    {
                        Console.WriteLine("Your answer is incorrect");

                    }
                    Console.WriteLine($"The score of player1 is : {player1}");


                } while (matrix[(card - 1) / 4, (card - 1) % 4] == matrix[(card2 - 1) / 4, (card2 - 1) % 4]);

                do
                {
                    if (player1 + player2 == 8)
                        break;
                    Console.WriteLine("player2 turn");
                    do
                    {


                        Console.WriteLine("chose a card");

                        card = PickCard();
                        card2 = PickCard();
                       // card3 = PickCard3();
                       // card4 = PickCard4();

                        if (matrix[(card - 1) / 4, (card - 1) % 4] == 0 || matrix[(card2 - 1) / 4, (card2 - 1) % 4] == 0)
                        {
                            Console.WriteLine("The cards you selected are already found");
                        }

                    } while (matrix[(card - 1) / 4, (card - 1) % 4]==0 || matrix[(card2 - 1) / 4, (card2 - 1) % 4] == 0);

                    if (matrix[(card - 1) / 4, (card - 1) % 4] == matrix[(card2 - 1) / 4, (card2 - 1) % 4])
                    {
                        player2++;

                        matrix[(card - 1) / 4, (card - 1) % 4] = 0;

                        matrix[(card2 - 1) / 4, (card2 - 1) % 4] = 0;

                        Console.WriteLine("Your answer is right You have another turn");
                    }
                    else
                    {
                        Console.WriteLine("Your answer is incorrect");

                    }
                    Console.WriteLine($"The score of player2 is : {player2}");



                } while (matrix[(card - 1) / 4, (card - 1) % 4] == matrix[(card2 - 1) / 4, (card2 - 1) % 4]);

                for (int i = 0; i < matrix.GetLength(0); i++)
                {
                    for (int j = 0; j < matrix.GetLength(1); j++)
                    {
                        Console.Write(" " + matrix[i, j]);

                    }
                    Console.WriteLine();
                }

            } while (player1 + player2 != 8);




            if (player1 > player2)
            {
                Console.WriteLine($"The winner is {player1}");
            }
            else
            {
                Console.WriteLine($"The winner is {player2}");
            }
        }
