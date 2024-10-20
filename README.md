using System;

internal class Program
{
    private string randomWord;
    private string guessedWord;

    public Program()
    {
        randomWord = WordCollection.GetRandomWord();
        SetGuessedWord();

        do
        {
            ShowGuessedWord();
            GetAnswer();
        } while (!AllWordGuessed());

        Console.WriteLine($"Congratulations! You've guessed the word: {randomWord}");
    }

    private void GetAnswer()
    {
        Console.WriteLine($"Give 1 letter [A-Z]: ");
        string letter = Console.ReadLine().ToLower();

        if (letter.Length == 1 && char.IsLetter(letter[0]))
        {
            if (IsContainedInRandomWord(letter))
            {
                Replace(letter);
            }
            else
            {
                Console.WriteLine("Incorrect guess, try again.");
            }
        }
        else
        {
            Console.WriteLine("Please enter a valid letter.");
        }
    }

    /// <summary>
    /// Mengganti simbol "_" pada guessedWord dengan huruf yang sesuai pada parameter "letter".
    /// </summary>
    private void Replace(string letter)
    {
        char[] guessedArray = guessedWord.ToCharArray();
        for (int i = 0; i < randomWord.Length; i++)
        {
            if (randomWord[i] == letter[0])
            {
                guessedArray[i] = letter[0];
            }
        }
        guessedWord = new string(guessedArray);
    }

    /// <summary>
    /// Mengecek apakah huruf yang diinput ada pada randomWord.
    /// </summary>
    private bool IsContainedInRandomWord(string letter)
    {
        return randomWord.Contains(letter);
    }

    private bool AllWordGuessed()
    {
        return !guessedWord.Contains("_");
    }

    private void SetGuessedWord()
    {
        guessedWord = new string('_', randomWord.Length);
    }

    private void ShowGuessedWord()
    {
        Console.WriteLine("Guess the word:");
        foreach (char c in guessedWord)
        {
            Console.Write($"{c} ");
        }
        Console.WriteLine();
    }

    static void Main(string[] args)
    {
        new Program();
    }
}

internal static class WordCollection
{
    public static string[] words = {
        "buyer",
        "flight",
        "wedding",
        "control",
        "development",
        "photo",
        "permission",
        "shopping",
        "candidate",
        "skill"
    };

    public static string GetRandomWord()
    {
        int r = new Random().Next(words.Length);
        return words[r];
    }
}

