# Upload File to Google Drive

This code uses the Google Drive API to upload a file to Google Drive.

## Prerequisites

* You need to have a Google Cloud Platform project and a service account key.
* You need to install the `googleapis` package.

## Usage

1. Create a file called `googlekey.json` and save your service account key in it.
2. Run the following command to install the `googleapis` package:

npm install googleapis


3. Run the following command to upload a file to Google Drive:

bun uploadFile.bun

Example
The following example code uploads the file snowplace.jpg to the Google Drive folder with the ID 1BDIkp5UWH1G-aDDT5Ep_4Bh9QlCs6BEr:
```

import fs from 'fs'
import { google } from 'googleapis'

const GOOGLE_API_FOLDER_ID = '1BDIkp5UWH1G-aDDT5Ep_4Bh9QlCs6BEr'

async function uploadFile() {
  try {
    const auth = new google.auth.GoogleAuth({
      keyFile: './googlekey.json',
      scopes: ['https://www.googleapis.com/auth/drive']
    })

    const driveService = google.drive({
      version: 'v3',
      auth
    })

    const fileMetaData = {
      'name': 'snowplace.jpg',
      'parents': [GOOGLE_API_FOLDER_ID]
    }

    const media = {
      mimeType: 'image/jpg',
      body: fs.createReadStream('./snowplace.jpg')
    }

    const response = await driveService.files.create({
      resource: fileMetaData,
      media: media,
      field: 'id'
    })
    return response.data.id
  } catch (err) {
    console.log('Upload file error', err)
  }
}

uploadFile()
  .then(data => {
    console.log(data);
    // https://drive.google.com/uc?export=view&id=
  })
  .catch(error => {
    console.error('Error:', error);
  });

```


## More Information

For more information, please see the following resources:

* [Google Drive API documentation](https://developers.google.com/drive/api/v3/)
* [googleapis package documentation](https://googleapis.dev/nodejs/googleapis/latest/)
I hope this helps! Let me know if you have any other questions.
