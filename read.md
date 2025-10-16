<!-- Appscript function used  -->
function doPost(e) {
  var data = e.parameter;

  // Match field names exactly as in your HTML form
  var name = data.Name || "";
  var email = data.Email || "";
  var message = data.Message || "";

  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var mainSheet = ss.getSheetByName("MAIN");

  // Create the sheet if missing
  if (!mainSheet) {
    mainSheet = ss.insertSheet("MAIN");
    mainSheet.appendRow(["Name", "Email", "Message", "Date"]);
  }

  // Append all form data + timestamp
  mainSheet.appendRow([name, email, message, new Date()]);

  return ContentService
    .createTextOutput("Success! Your message has been recorded.")
    .setMimeType(ContentService.MimeType.TEXT);
}
<!-- the above is for an external html  -->
<!-- For an internal  html  -->
function AddRecord(name) {
  
  var ss= SpreadsheetApp.getActiveSpreadsheet();
  var mainSheet = ss.getSheetByName("MAIN");
  mainSheet.appendRow([name, new Date()]);
  
}

function startForm()
{
 var form = HtmlService.createHtmlOutputFromFile('AddForm');
 SpreadsheetApp.getUi().showModalDialog(form, 'Add Record');
  
  
}

function addMenu()
{
 var menu = SpreadsheetApp.getUi().createMenu('Custom');
 menu.addItem('Add Record Form', 'startForm');
 menu.addToUi();
  
}

function onOpen(e)
{
  
 addMenu(); 
}
<!-- the following should be noted  -->
the above is sensitive case and the details should be the same 