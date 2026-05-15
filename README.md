function splitPDF() {

  var fileId = "YOUR_FILE_ID";

  var file = DriveApp.getFileById(fileId);

  var blob = file.getBlob();

  var response = UrlFetchApp.fetch(
    "YOUR_RENDER_URL/split",
    {
      method: "post",
      payload: {
        file: blob
      },
      muteHttpExceptions: true
    }
  );

  var zipBlob = response.getBlob();

  zipBlob.setName("split_files.zip");

  DriveApp.createFile(zipBlob);

  Logger.log("PDF Split Success");
}
