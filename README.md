# Election-Analysis

### 1. Overview of Election Audit:
#### After summarizing election data for candidates and submitting the results to the election commision, we were tasked with analyzing the same data set for counties. Our goal is to produce the following:

* The voter turnout for each county
* The percentage of votes from each county out of the total count
* The county with the highest turnout

#### In addition to gathering the county data, we also needed to save results in a txt file.

### 2. Election-Audit Results:
1. How many votes were cast in this congressional election?
    * There were a total of 369,711 votes
    
    * We found results by looping through the data and tallying 1 to the total_votes variable. See sample code below:
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
    
2. Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.
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

### 3. Election-Audit Summary:
#### An overview of the results are outlied below:
![Election Results](https://github.com/maldonado91/Election-Analysis/blob/main/Resources/ElectionSummary.PNG)

#### This piece of code can be used to for more than just candidates and counties election results depending on what is available. Example:
1. If we have additional columns like maybe year, political party, etc, we can summarize the results just like we did candidate and county. We would just need to create respective varaible for any new column field and include in the for loop that tallies the vote counts.
2. Assuming we add more columns (i.e year, political party) we can calculate additional metrics. Possibilites include the average voter turnout by year or average turnout by political party.
#### Finalized python code can be found [here](https://github.com/maldonado91/Election-Analysis/blob/main/PyPoll_Challenge.py)
