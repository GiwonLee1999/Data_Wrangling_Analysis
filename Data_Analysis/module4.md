# Module 4: Data verification

Sources of errors: Did you use the right tools and functions to find the source of the errors in your dataset?

Null data: Did you search for NULLs using conditional formatting and filters?

Misspelled words: Did you locate all misspellings?

Mistyped numbers: Did you double-check that your numeric data has been entered correctly?

Extra spaces and characters: Did you remove any extra spaces or characters using the TRIM function?

Duplicates: Did you remove duplicates in spreadsheets using the Remove Duplicates function or DISTINCT in SQL?

Mismatched data types: Did you check that numeric, date, and string data are typecast correctly?

Messy (inconsistent) strings: Did you make sure that all of your strings are consistent and meaningful?

Messy (inconsistent) date formats: Did you format the dates consistently throughout your dataset?

Misleading variable labels (columns): Did you name your columns meaningfully?

Truncated data: Did you check for truncated or missing data that needs correction?

Business Logic: Did you check that the data makes sense given your knowledge of the business? 

### Documentation
- Track changes when data cleaning.
- Recover data-cleaning errors.
- Create a new table rather overwriting.

1) recalling the errors that were cleaned and
2) Informing others of the changes -- assume that the data errors aren't fixable.

### Changelogs: Check the history of changes done in the data
Excel->File->version history
SQ:->Query history

### Version control system
1. A company has official versions of important queries in their version control system.
2. An analyst makes sure the most up-to-date version of the query is the one they will change. This is called syncing
3. The analyst makes a change to the query.
4. The analyst might ask someone to review this change. This is called a code review and can be informally or formally done. An informal review could be as simple as asking a senior analyst to take a look at the change.
5. After a reviewer approves the change, the analyst submits the updated version of the query to a repository in the company's version control system. This is called a code commit. A best practice is to document exactly what the change was and why it was made in a comments area. Going back to our example of a query that pulls daily revenue, a comment might be: Updated revenue to include revenue coming from the new product, Calypso.
6. After the change is submitted, everyone else in the company will be able to access and use this new query when they sync to the most up-to-date queries stored in the version control system.
7. If the query has a problem or business needs change, the analyst can undo the change to the query using the version control system. The analyst can look at a chronological list of all changes made to the query and who made each change. Then, after finding their own change, the analyst can revert to the previous version.
8. The query is back to what it was before the analyst made the change. And everyone at the company sees this reverted, original query, too.
  
 



