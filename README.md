# BackgroundErase API Javascript Integration

Javascript wrapper for the BackgroundErase API.

## Installation
```bash
git clone https://github.com/PramaLLC/ben-api-javascript-integration
cd ben-api-javascript-integration
npm install
```

## Generate API Key 
You must have an active business subscription which can be found at https://backgrounderase.com/pricing. To generate your API key navigate to
https://backgrounderase.com/account and scroll to the 'API Access' section then press 'Generate Key'.

## Example code inside example.js

```javascript
const fs = require('fs');
const path = require('path');
const { predictImage } = require('./main');

async function main() {
  try {
    const apiKey = 'your_ben_api_token'; // Replace with your API token
    const apiUrl = 'https://api.backgrounderase.net/v2';
    
    // Load image file
    const inputPath = path.join(__dirname, 'image.jpg'); // Replace with your image path
    const originalBuffer = fs.readFileSync(inputPath);
    
    // Get prediction
    const result = await predictImage(originalBuffer, apiKey, apiUrl);
    
    if (!result) {
      console.error('Failed to get a valid result from predictImage.');
      return;
    }
    
    // Save results
    const { mask, foreground } = result;
    fs.writeFileSync(path.join(__dirname, 'result.png'), foreground);
    fs.writeFileSync(path.join(__dirname, 'mask.png'), mask);
    
  } catch (err) {
    console.error('Error:', err);
  }
}

main();
```

## To run the example code
```bash
node example.js
```


## API documentation
For full API documentation visit: https://backgrounderase.com/docs
