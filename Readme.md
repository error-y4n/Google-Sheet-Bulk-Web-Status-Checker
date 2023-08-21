Open Google sheet 

Input Your Bulk Website In Column A

Click On Extension

App Script

Past This Code 




function checkUrls() {
  // get the number of rows in the sheet
  var sheet = SpreadsheetApp.getActiveSheet();
  var numRows = sheet.getLastRow();
  
  // loop through each row
  for (var i = 1; i <= numRows; i++) {
    // get the URL in column A
    var url = sheet.getRange(i, 1).getValue();
    
    // try to fetch the URL
    try {
      var response = UrlFetchApp.fetch(url);
      var statusCode = response.getResponseCode();
      
      // check the status code
      if (statusCode >= 300 && statusCode <= 399) {
        // input the error in column B
        sheet.getRange(i, 2).setValue("Redirection error: status code " + statusCode);
      } else if (statusCode >= 400 && statusCode <= 499) {
        // input the error in column B
        sheet.getRange(i, 2).setValue("Client error: status code " + statusCode);
      } else if (statusCode >= 500 && statusCode <= 599) {
        // input the error in column B
        sheet.getRange(i, 2).setValue("Server error: status code " + statusCode);
      } else {
        // set the value in column B to "website is okay"
        sheet.getRange(i, 2).setValue("website is okay");
      }
    } catch (e) {
      // input the error in column B
      sheet.getRange(i, 2).setValue("Error: " + e);
    }
  }
}


Save 
Run This Code 
And Check Your Sheet
