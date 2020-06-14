# TFT_High ELO rank data analysis



### Workflow example

1. Data Parsing(Load Data)

   ```python
   # example
   chall_game = pd.read_csv('./dataset/tft-match-data/TFT_Challenger_MatchData.csv')
   ```

2. Data Consistency Check

   1) Check consistency - index

   ```python
   # check first_5 data
   chall_game.head()
   ```

   2) Check Ranking 1st to 8th place by game for each

   ```python
   # Challenger
   data_cons = chall_game.groupby('gameId')['Ranked'].count().tolist()
   err_game = []
   
   for i in range(len(data_cons)):
       if data_cons[i] != 8:
           print(chall_game.groupby('gameId')['Ranked'].count().keys()[i])
           err_game.append(chall_game.groupby('gameId')['Ranked'].count().keys()[i])
   ```

   3) delete that dose not match the consistency

   ```python
   # Delete data that does not match the consistency
   
   chall_game = chall_game[chall_game['gameId'] != err_game[0]]
   ```

   