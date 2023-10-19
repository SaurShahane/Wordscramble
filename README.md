#include <string.h>
#include <stdlib.h>
#include <time.h>
#include <ctype.h>
#include <stdbool.h>

void scramble(char *s);

int main()
{
  srand(time(NULL));

  char words[][100] = {"friends", "engineers", "water", "hello","remember","programming"};
  char original[100];
  char scrambled[100];
  char answer[100];

  int random_index = rand() % 4; // Choose a random word from the array
  strcpy(original, words[random_index]);
  strcpy(scrambled, original);
  scramble(scrambled);

  bool game_over = false;
  do
  {
    printf("Unscramble the word: %s\n\n", scrambled);
    printf("Answer: ");
    scanf("%s", answer);

    if (strcmp(answer, original) == 0)
    {
      printf("\nYou got it!\n\n");
      game_over = true;
    }
    else
    {
      printf("\n sorry! Try again!\n\n");
    }

  } while (!game_over);

  return 0;
}

void scramble(char *s)
{
  int length = strlen(s);

  for (int i = 0; i < length; i++)
    s[i] = tolower(s[i]);

  if (length == 1)
    return;

  if (length == 2)
  {
    char temp = s[0];
    s[0] = s[1];
    s[1] = temp;
    return;
  }
  char original[length + 1];
  strcpy(original, s);
   double diff = 0;
  bool same_start = false;
  bool same_end = false;
  int times_stuck = 0;
  do
  {

    int i = 0;
    while (i < length)
    {

      int pos1 = rand() % length;
      int pos2 = rand() % length;

      if (pos1 != pos2)
      {
        char temp = s[pos1];
        s[pos1] = s[pos2];
        s[pos2] = temp;
        i++;
      }
    }
    int differences = 0;
    for (int j = 0; j < length; j++)
      if (original[j] != s[j]) differences++;


    same_start = s[0] == original[0];
    same_end = s[length - 1] == original[length - 1];

    times_stuck++;
  } while (((same_start && same_end) || (diff < 0.5)) && (times_stuck < 100));

}
