# Call-Reports-of-US-Banks.
This project aims to analyse call report data from US Banks to form a time-consistent series of deposits (demand, brokered, and time), loans (C&I, personal, and real estate loans), and mortgage-backed securities, and analyse their trends across small, medium, large, and very large banks.

The whole data processing pipeline is divided into 5 parts.

Part A: It unzips the downloaded files into the txt files. Each folder corresponds to a quarter, and the folders are renamed YYYY-MM-DD.

PART B: We create two dynamic files, one for the reporter information and the other for the master dictionary. For the reporter information, the code first reads the first quarter POR file and stores it in an Excel file named(suppose) Reporter_infor_file. When it reads the next quarter, it updates the Reporter_infor_file. Now, here we get a summary of the changes in the reporter information file that are taking place over the quarters. We can see that a significant number of banks are removed each year, while only a few are added. We can perform this analysis for all the information, including zip code, bank filing type, bank name, and even the bank location. The summary is stored in the reporter_updates_log file.

We are conducting a similar exercise for the master dictionary, which contains all the variable codes and variable names for RC, RI, and SU. This dictionary is crucial in tracking changes to codes over time and in mapping them to variables in the later stages of the project.

PART C: In this part, we convert the text files of the schedules to parquet files. The parquet files technique is similar to that of CSV or Excel files, but is almost 5 times faster in operation. The parquet files are a hybrid model of row and columnar data, unlike Excel/CSV files. They are machine-readable in raw format and not human-readable.

PART D: In this part, first, we create a dictionary of all the important codes we are interested in. These are the codes of variables that we would like to keep at the end of the file. If we would like to analyse more variables or only one variable, we can easily do so by editing this dictionary. Next, we read all the parquet schedule files for each quarter from the Parq. Quarters folder and merge them on the basis of the important_codes to create a smaller parq. files and then finally convert those to CSV files. 

PART E: Here, we are creating a time-consistent series of Assets, including Deposits (Time Deposits, Demand Deposits, and Brokered Deposits), Loans (Personal, Commercial, and Industrial Loans, Real Estate Loans), and Mortgage-Backed Securities. The various call report codes for these components have changed over time, with significant changes occurring between 2008 and 2011. Therefore, tracking down all those changes and making the necessary adjustments is absolutely necessary for accurate trend analysis.



