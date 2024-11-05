using System;
using System.Collections.Generic;

public class TextFunctions
{
    public static int RuznychPismen(string text) /*a*/
    {
        HashSet<char> uniqueLetters = new HashSet<char>();
        foreach (char c in text)
        {
            if (char.IsLetter(c))
                uniqueLetters.Add(char.ToLower(c));
        }
        return uniqueLetters.Count;
    }

    public static int PocetSlov(string text) /*b*/
    {
        int count = 0;
        bool inWord = false;
        foreach (char c in text)
        {
            if (char.IsLetter(c))
            {
                if (!inWord)
                {
                    inWord = true;
                    count++;
                }
            }
            else            
                inWord = false;
        }
        return count;
    }

    public static string PrvniSlovo(string text, int position) /*c*/
    {
        int start = -1, end = -1;

        if (position < 0 || position >= text.Length)
            return "";

        if (char.IsLetter(text[position]))
        {
            start = position;
            while (start > 0 && char.IsLetter(text[start - 1]))
                start--;
            end = position;
            while (end < text.Length - 1 && char.IsLetter(text[end + 1]))
                end++;
        }
        else
        {
            int i = position;
            while (i < text.Length && !char.IsLetter(text[i]))
                i++;
            if (i < text.Length && char.IsLetter(text[i]))
            {
                start = i;
                while (i < text.Length && char.IsLetter(text[i]))
                    i++;
                end = i - 1;
            }
        }

        return start != -1 && end != -1 ? text.Substring(start, end - start + 1) : "";
    }

    public static string NejdelsiSlovo(string text) /*d*/
    {
        int maxLength = 0;
        string longestWord = "";

        int i = 0;
        while (i < text.Length)
        {
            while (i < text.Length && !char.IsLetter(text[i])) i++;

            int start = i;
            while (i < text.Length && char.IsLetter(text[i])) i++;
            int length = i - start;

            if (length > maxLength)
            {
                maxLength = length;
                longestWord = text.Substring(start, length);
            }
        }
        return longestWord;
    }

    public static string NejvetsiSlovo(string text) /*e*/
    {
        string largestWord = "";

        int i = 0;
        while (i < text.Length)
        {
            while (i < text.Length && !char.IsLetter(text[i])) i++;

            int start = i;
            while (i < text.Length && char.IsLetter(text[i])) i++;
            string word = text.Substring(start, i - start);

            if (word.CompareTo(largestWord) > 0)
                largestWord = word;
        }
        return largestWord;
    }

    public static void Main()
    {
        string s1 = "Alena ma 2 ruce.";
        int ruznych = RuznychPismen(s1);
        int pocet = PocetSlov(s1);
        string s2 = PrvniSlovo(s1, 2);
        string s3 = PrvniSlovo(s1, s1.Length - 1);
        string s4 = NejdelsiSlovo(s1);
        string s5 = NejvetsiSlovo(s1);
        string s6 = "Mama ma 2 ruce a v ruce hul";

        Console.WriteLine($"Ruznych pismen: {ruznych}");
        Console.WriteLine($"Pocet slov: {pocet}");
        Console.WriteLine($"Prvni slovo na pozici 2: {s2}");
        Console.WriteLine($"Prvni slovo na posledni pozici: {s3}");
        Console.WriteLine($"Nejdelsi slovo: {s4}");
        Console.WriteLine($"Nejvetsi slovo: {s5}");
    }
}
