# Object Detection


Object detection engines find instances of real-world objects such as people, animals, and buildings in videos. Object detection algorithms not only recognize and classify every object in an image, they determine the location by drawing a bounding box around it. The basic object detection engine output features an array of objects with data attributes associated with individual observations of detected items within a specified time increment. 
 
The following tables provide the supported input and output models for object detection engines. The Input Structure specifies the data being passed to the engine to perform the request. All expected data fields in the file returned from the engine are described in the Output Structure.

## Input Data Structure ##

Input assets to object detection engines typically take the form of video files. To ensure your engine can accept and process tasks, be sure your engine’s supported file formats (specified in the build manifest) align with those used by Veritone. A preprocessing step of extracting the frames from the input video is required before object detection processing can begin. 
The object detection engine input requirements are described in the table below.

<table>
  <tr>
    <td width="20%"><h3 class="text-left">Data Structure</h3></td>
    <td width="80%"><h3 class="text-left">Description</h3></td>
  </tr>
  <tr>
   <td align="right" valign="top"><b>Task Payload</b><br>object
</td>
    <td>The payload (provided by Veritone) with data that describes the task to be completed by the engine. See the sample Task Payload in the Engine Construction Guidelines for more information.
</td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>Content-Type</b><br>string
</td>
    <td>The format (MIME type) of the input file. 

<code>"contentType": "video/mp4"</code></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>Input Asset URI</b><br>string
</td>
    <td>The signed URI of the input asset to be transcribed. This property must use a URI located on Veritone’s S3 as the value. 
     
<code>"signedUri": "https://inspirent.s3.amazonaws.com/assets/39528568/ 909b4ac0-3218-4026-812d-afca91ba0d14.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7L6G7PCOOOLA7MQ%2F20171116%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20171116T180716Z&X-Amz-Expires=604800&X-Amz-Signature=26447f611793e8a7e6b510b174d7ffd0b94a84fda9cbf59a79a8e936f17dc009&X-Amz-SignedHeaders=host"</code></td>
  </tr>
</table>

### Output Data Structure ###

When task processing is complete, your engine will write an output summary of the analysis as a JSON file and send it to Veritone to create a new asset. The output structure consists of an array of time-series objects with data attributes for each object found in the input file. Each result in the series includes a label for the detected object, the starting and ending times that the object was identified in the input file, and a confidence score. 
To generate an output file, use the data structure described in the table below and save the document with the extension .json. Once your output file is created, call the UploadEngineResult GraphQL mutation to upload the results. (See the Engine Construction Guidelines for full request details.)

<table>
  <tr>
    <td width="18%"><h3 class="text-left">Data Structure</h3></td>
    <td width="57%"><h3 class="text-left">Description</h3></td>
    <td width="25%"><h3 class="text-left">Example</h3></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>series</b><br>array<br>required</td>
    <td>The root object field of the results array. </td>
    <td><code>series: [</code></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>found</b><br>string<br>required</td>
    <td>A label that identifies the detected object.</td>
    <td><code>found: "minivan"</code></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>start</b><br>integer<br>required</td>
    <td>The time in milliseconds from the beginning of the input file that the object was first identified.</td>
    <td><code>start: "4000"</code></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>end</b><br>integer<br>required</td>
    <td>The time in milliseconds from the beginning of the input file that the object was last identified.</td>
    <td><code>end: "15000"</code></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>salience</b><br>float<br>optional</td>
    <td>The estimated probability that the detected object is correctly identified. Scores range from 0-100, with a higher score indicating greater correlation.</td>
    <td><code>salience: 88.5096206665039</code></td>
  </tr>
  <tr>
    <td align="right" valign="top"><b>bounding poly</b><br>object<br>optional</td>
    <td>The coordinates of the bounding box around the detected object. The left (x-coordinate) and top (y-coordinate) are coordinates representing the top and left sides of the bounding box. The width and height values represent the dimensions of the bounding box as a ratio of the overall image dimension.</td>
    <td><code>boundingPoly: {
      left: 0.318888902664,
      top: 0.493333339691,
      width: 0.25,
      height: 0.334814816713,
 }</code></td>
  </tr>
</table>

## Sample Object Detection Output Data Structure ##

```json
{
  "series": [
    {
      "found": "outdoor",
      "start": 0,
      "end": 109050,
      "confidence": 825
    },
    {
      "found": "minivan",
      "start": 3375,
      "end": 5875,
      "confidence": 763
    },
    {
      "found": "Chevrolet",
      "start": 3375,
      "end": 4375,
      "confidence": 664
    },
    {
      "found": "armrest",
      "start": 11625,
      "end": 100125,
      "confidence": 800
    }
  ]
}
```

## Upload Engine Results ##

Once the output file is created, make a request to the UploadEngineResult mutation to upload the file and create a new asset. The table below outlines the fields accepted in the request payload. For complete request details, refer to the Engine Construction Guidelines. 

<table>
  <tr>
    <td width="18%"><h3 class="text-left">Field</h3></td>
    <td width="57%"><h3 class="text-left">Description</h3></td>
    <td width="25%"><h3 class="text-left">Example</h3></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>content-type</b><br>header<br>string</td>
    <td>A header that specifies the content type of the request. Enter multipart/form-data as the value.</td>
    <td><code>content-type: multipart/form-data</code></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>file</b><br>form<br>string</td>
    <td>The path of the file to upload.</td>
    <td><code>file=@/Users/bobjones/Downloads/your-filename.json</code></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>filename</b><br>form<br>string</td>
    <td>The name of the file to upload. The value must match the name of the saved file.</td>
    <td><code>filename=your-filename.json</code></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>taskId</b><br>body<br>string</td>
    <td>The Task ID received in the Task Payload.</td>
    <td><code>taskId: "e0d2ff71-503f-4ace-a214-3bb941425fd6-b4e26652-eba4-4740-91f8-1c59b18811ef"</code></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>contentType</b><br>body<br>string</td>
    <td>The MIME type of the file to upload. Specify "application/json" as the value.</td>
    <td><code>contentType: "application/json"</code></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>assetType</b><br>body<br>string</td>
    <td>The type of asset to create. Specify “object” as the value.</td>
    <td><code>assetType: "object"</code></td>
  </tr>
  <tr valign="top">
    <td align="right"><b>completeTask</b><br>body<br>Boolean</td>
    <td>A Boolean that marks the task as complete. Set the value to true.</td>
    <td><code>completeTask: true</code></td>
  </tr>
</table>
