# Automated-Co-op-Enrolment-Confirmation-Letter-Generator
This project automates the creation of personalized Co-op enrollment confirmation letters directly from Google Sheets using Google Apps Script &amp; Google Docs.  It was designed to save time and reduce errors when generating letters for 100+ students, eliminating the need for manual copy-paste edits in Google Docs.

This tool was built as part of a summer job to streamline the Co-op office’s workflow. Staff can now generate dozens of confirmation letters in seconds instead of manually editing templates for each student. To make the script understandable for non-technical users I added clear in-code comments indicating which parts of the script can and cannot be changed, making it easy for my coworkers to adapt without breaking the automation.

## Technology Used
- Google Apps Script (JavaScript-based)
- Google Sheets & Docs API
- Google Drive API

Below is a guide I prepared for my coworkers following the completion of this project.

## **How Do You Use this Automation?**
1. Open the spreadsheet associated with the Google Apps Script.
2. An “Automate” menu appears at the top.
3. Select the rows you want to generate a letter for. 
4. Click “Generate Co-op Letter(s)” from the “Automate” menu.
5. Select what type of letter you want to generate.
6. Wait. Each letter takes 1 second to generate. A message will appear once the automation has been completed. 
7. The selected letters will be generated into a PDF format and saved into the specified Google Drive folder. 
8. Every time a letter is generated, it creates a timestamp of when that letter was generated, link to the generated letter, and type of letter that was generated to the right side of the sheet. 

## **What You Can Safely Edit**
*Note: JavaScript is case-sensitive which means anything you rename or change in the document template or spreadsheet should have an exact replication in the Apps Script. 
Google Doc Template IDs*

The script references two Google Doc templates by their IDs (the long string in the document URL).
If you update or change your template, copy the new document’s ID and replace it: 
const doc1Id = 'YOUR_NEW_TEMPLATE_1_ID'; 
const doc2Id = 'YOUR_NEW_TEMPLATE_2_ID'; 

### Google Drive Folder ID
To save the generated files to a different folder, copy that folder’s ID from its URL (after /folder/) and replace this line: 
const folderId = "1yMsqkG9z8hpwCSoFLjroIPlPGWj9aGhY";

### Changing the Names of the Files Generated
When the letters are generated, they are saved with the name “Co-op Enrolment Confirmation Letter - [Student Name]”.
If you want to change how these letters are named (for example, to include employer name or program name), look for this line in the script (line 98):
const newFileName = `Co-op Enrolment Confirmation Letter   -${studentName}`;

### Adding a New Column in the Spreadsheet
If your sheet and template include a new variable (i.e. jobTitle), you’ll need to:
Add a new body.replaceText AFTER the last body.replaceText. For jobTitle:
body.replaceText("{{jobTitle}}", rowData["jobTitle"]);

Make sure the new variable exists (i.e. jobTitle):
- In your sheet header (no extra spaces or typos)
- As a placeholder (in curly brackets) in your template Doc → {{jobTitle}}

## What You Should Not Change
*Unless you know JavaScript, do not change:*

1. Anything labeled “DO NOT CHANGE” in the code.
2. The order of replaceText() calls. 
3. Placeholder names unless you also update your Google Doc to match. 
4. DO NOT copy paste placeholders in the document template as this will carry over any hidden formatting, making it unreadable by Apps Script. If you are copy pasting anything in the template, ensure you remove formatting:
- Highlight the text you have copy pasted.
- Navigate to “Format” on Google Docs. 
- Click “Clear Formatting”). 




