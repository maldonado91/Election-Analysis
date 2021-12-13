# Election-Analysis

### 1. Overview of Election Audit:
#### After summarizing election data for candidates and submitting the results to the election commision, we were tasked with analyzing the same data set for counties. Our goal is to produce the following:

* The voter turnout for each county
* The percentage of votes from each county out of the total count
* The county with the highest turnout

In addition to gathering the county data, we also needed to save results in a txt file.

### 2. Election-Audit Results:
1. How many votes were cast in this congressional election?
    * There were a total of 369,711 votes
    
    * We found results by looping through the data and tallying 1 to the total_votes variable. See sameple code below:
    ```
      # Read the csv and convert it into a list of dictionaries
      with open(file_to_load) as election_data:
          reader = csv.reader(election_data)

          # Read the header
          header = next(reader)

          # For each row in the CSV file.
          for row in reader:

              # Add to the total vote count
              total_votes = total_votes + 1
    ```
    
2. Provide a breakdown of the numnber of votes and the percentage of total votes for each county in the precinct.
   * The breakdown is as follows:
      * Jefferson: 38,855 - 10.5%
      * Denver: 306,055 - 82.8%
      * Arapahoe: 24,801 - 6.7%
      
   * By adding up the total votes through the loop above, we then added all the votes for each respective county. See code below:
   ```
        # county does not match any existing county in the county list.
        if county_name not in county_options:

            # 4b: Add the existing county to the list of counties.
            county_options.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1
    ```
    
   * This allowed us to do the math in calculating totals and percentages
   
3. Which county had the largest number of votes
   *  The county with the largest amount of votes was Denver with 306,055 (82.8%)
   
4. Provide a breakdown of the number of votes and the percentage of the total votes each candidate received
   * Identical to counties, we added up the total votes through the loop above. See code below:
   ```
        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1
   ```

5. What candidate won the election, what was their vote count, and what was their percentage of the total votes?
   * The winning candidate was Diana DeGette with 272,892 votes (73.8%)

#### An overview of the results are outlied below:
![Election Results](https://github.com/maldonado91/Election-Analysis/blob/main/Resources/ElectionSummary.PNG)

#### After refactoring the code the analysis for all stock 2017 and 2018 displayed the exact same results. 
![All-Stocks_2017](https://github.com/maldonado91/Stock-Analysis/blob/main/Resources/All_Stocks_2017.png) ![All-Stocks_2018](https://github.com/maldonado91/Stock-Analysis/blob/main/Resources/All_Stocks_2018.png)
#### However, the run time was much different in both instances. We saw much faster times, therefore, acheiving our goals of enhancing code performance.
#### Here is 2017
Before ![Run_Time2017_Before](https://github.com/maldonado91/Stock-Analysis/blob/main/Resources/VBA_Challenge_2017_Before.PNG) After ![Run2017_Time_After](https://github.com/maldonado91/Stock-Analysis/blob/main/Resources/VBA_Challenge_2017.PNG)
#### Here is 2018
Before ![Run_Time2018_Before](https://github.com/maldonado91/Stock-Analysis/blob/main/Resources/VBA_Challenge_2018_Before.PNG) After ![Run_Time2018_After](https://github.com/maldonado91/Stock-Analysis/blob/main/Resources/VBA_Challenge_2018.PNG)

#### Changing the code to run throught the data once was extremely useful. See below 'for loop' used in macro:
    ''2b) Loop over all the rows in the spreadsheet.
    For i = 2 To RowCount
    
        '3a) Increase volume for current ticker
        tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 8).Value
        
        '3b) Check if the current row is the first row with the selected tickerIndex.
         If Cells(i - 1, 1).Value <> tickers(tickerIndex) And Cells(i, 1).Value = tickers(tickerIndex) Then
         
            tickerStartingPrices(tickerIndex) = Cells(i, 6).Value
            
        End If
        
        '3c) check if the current row is the last row with the selected ticker
         'If the next row’s ticker doesn’t match, increase the tickerIndex.
         If Cells(i + 1, 1).Value <> tickers(tickerIndex) And Cells(i, 1).Value = tickers(tickerIndex) Then
         
            tickerEndingPrices(tickerIndex) = Cells(i, 6).Value
            '3d Increase the tickerIndex.
            tickerIndex = tickerIndex + 1
            
         End If
    
    Next i
#### Before we ran through the two separate loops to acheive the same output. See below 'for loop' used in macro:
    For i = 0 To 11
    
        ticker = tickers(i)
        totalVolume = 0
        
        'Loop through the data
        Worksheets(yearValue).Activate
        For j = 2 To rowEnd
            
            If Cells(j, 1).Value = ticker Then
            
                totalVolume = totalVolume + Cells(j, 8).Value
                
            End If
            
            'Find the starting price for the current ticker
            If Cells(j - 1, 1).Value <> ticker And Cells(j, 1).Value = ticker Then
                
                startingPrice = Cells(j, 6).Value
                
            End If
            
            'Find ending price for the current ticker
            If Cells(j + 1, 1).Value <> ticker And Cells(j, 1).Value = ticker Then
                
                endingPrice = Cells(j, 6).Value
                
            End If
            
         Next j
         
         'Outout the data for the current ticker
         Worksheets("All Stock Analysis").Activate
         Cells(4 + i, 1).Value = ticker
         Cells(4 + i, 2).Value = totalVolume
         Cells(4 + i, 3).Value = endingPrice / startingPrice - 1
         
    Next i
#### You can find final project VBA code [here.](https://github.com/maldonado91/Stock-Analysis/blob/main/VBA_Challenge_Complete.vbs)

### 3. Summary:
#### What are the advantages or disadvantages of refactoring code?
The advantages are certainly improved code. We manageed to shrink the amount of code used and made the macro more readable.

#### How do these pros and cons apply to refactoring the original VBA script?
In this particular example we established quicker run times which will allow us the potential to analyze more information and additional years. We were able to leverage arrays to provide our output and we only had to run through the rows of tickers one time. Like the code above shows, we specifically used a for loop to run through our data one time as opposed to once for every ticker in the data set. 

