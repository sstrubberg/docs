# Taxonomy

## Engine Types
There are three types of engines in aiWare: adapter, cognition, and aggregator.  

### Adapter / Ingestion
Adapter engines, also known as ingestion engines, bring data from other sources into aiWare.  The data can either be a real-time stream or a bounded file, and can be structured or unstructured.  Once the data is in aiWare, it can be processed by cognitive engines to derive insights for your end users.

The are two types of adapters: push and pull.

#### Push Adapter
A push adapter is an engine that listens for data from an external source and brings it into aiWare.  An example of this type of adapter is one that listens for a stream or RSS feed and sends the data to other engines in aiWare.

#### Pull Adapter
A pull adapter retrieves data from a source, typically a URI, and brings it into aiWare.  Most adapters are pull adapters.

Veritone provides several pull adapters that are available to all users, including some to pull content from Amazon S3, YouTube, Google Drive, Box, Dropbox, RSS and FTP.  There is also a File Upload adapter that allows you to select a file from your personal computer.  

### Cognition
Cognition engines are the workhorses of aiWare.  They process the data brought in by adapters and employ sophisticated algtorithms and machine learning techniques to produce even more data from which you can derive actionable insights. Examples of what a cognition engine does include natural language processing, transcription, and object detection.

You can build a pipeline of cognition engines, to be run sequentially or in parallel, each one enhancing the target output data set.  For example, a pipeline could include the following engines:
1. Ingest video stream (Adapter)
2. Transcribe video to text (Cognitive)
3. Translate to another language (Cognitive)
4. Do sentiment analysis (Cognitive)

### Aggregator
Aggregator engines consolidate the outputs from all the cognition engines run within a pipeline and creates a new output data set for use in aiWare.  While the inputs to cognition engines come from a single source, usually the ingested data from an adapter or the output from another cognition engine, the inputs to aggregator engines come from multiple sources.  An aggregator can either be intracategory, processing results from a single cognition capability, or intercategory, working across two or more capabilities.

Below is a sample pipeline that includes an intracategory aggregator engine at the end.

1. Ingest audio stream (Adapter)
2. Transcribe audio using a clould engine provider A (Cognition)
3. Transcribe audio using a clould engine provider B (Cognition)
4. Transcribe audio using a clould engine provider C (Cognition)
5. Select the best result from all 3 transcripts (Aggregator)


## Cognitive Engine Classes
Cognition engines are categorized into engine classes.  Below is a table of our currently suppored engine classes

Class | Description | Inputs | Examples
--- | --- | --- | ---
Speech | Applies artificial intelligence to human lanuguage to locate, capture, identify, and categorize spoken word. | Audio data | Transcription, language detection
Text | Applies aritificial intelligence to text inputs. | Text data | Language translation, text-to-speech, content categorization
Vision | Processes images to identify, segment, and extract details. | Pictures and videos | Object recognition, visual moderation (tagging)
Biometrics | Analyzes the unique physical identifiers for identiication and categorization. | Pictures, videos and biometric data (fingerprints, scans) | Face detection, facial recognition
Audio | Identifies audio signatures and captures patterns from sounds. | Audio data | Audio recogition, music detection
Data | Extracts time-saving actionable insights from data. | All kinds of data | Recommendation, telematics
Transformation | Transforms input to produce an enhanced or modified data set.  | All kinds of data | Visual redaction, transcoding

## Engine Capabilities
Under each engine class is a set of capabilities, which are defined by the engine output.  This table presents the currenty supported engine capabilities on aiWare.  

Class | Capability | Description
--- | --- | ---
Speech | Transcription | Converts speech audio to text.
Speech | Language Identification | Identifies the natural human language(s) spoken in an audio file.
Speech | Speaker Separation	| aka Diarization. Partitions an input audio stream into segments according to who is speaking when.
Speech | Keyword Spotting	| Finds specific words in an audio recording, without producing a transcript.
Text | Translation | Translates natural language from a text source.
Text | Text-to-Speech | Generates spoken word from text. Configurations may include output voice gender and accent.
Text | Entity Extraction | aka Named-entity recognition. Classifies named entities located in unstructured text into pre-defined categories such as people, organizations and locations.
Text | Summarization | Generates a summar of written text.
Text | Content Classification | Categorizes one or multiple documents according to a pre-defined ontology.
Text | Language Identification | Detects one or multiple natural languages in text.
Text | Sentiment | Classifies text according to sentiment. May include a score representing negative, neutral or positive, or include a wider breadth of tags such as "happy" or "excited".
Vision | General Object Detection | Detects one or multiple objects or concepts in an image or video from a general/broad ontology, eg. "car" or "person".
Vision | Specialized Object Detection | Detects one or multiple objects or concepts in an image or video from a narrow ontology, eg. Vehicles, Logos, Food, Art, Apparel, Landmark.
Vision | Image Classification | Classifies the entire image (not objects within an image). eg. "landscape" or "basketball game".
Vision | Color | Recognizes colors in an image or video.
Vision | Visual Moderation | Tags an image or video which likely contains explicit content.
Vision | Text Recognition (OCR) | aka Optical Character Recognition. Converts alphanumeric characters in a document, image or video, to text.
Vision | License Plate (ALPR) | Produces a text string of alphanumeric characters for each license plate recognized in an image or video.
Vision | Scene Break | Segments a video by identifying each instance of a scene change.
Biometrics | Face Detection | Detects the presence of one or multiple faces in an image or video.
Biometrics | Face Recognition | Identifies one or multiple people in an image or video by associating each individual's face to their name.
Audio | Audio Fingerprinting | Recognizes a specific audio segment, eg. a radio advertisement, as it appears in a longer audio file or on its own.
Audio | Audio Recognition | Recognizes sound segments in an audio file, eg. 'gunshot', 'ad' or 'crying baby'.
Data | Correlation | Associates two data products based on some commonality, such as occurence over time. For example, may associate weather data on a given date with stock prices on that date.
Data | Geolocation | Identifies the geographic location of a person or object in the real world or some virtual equivalent.
Transformation | Transcoding | Converts one input file format to another.
Transformation | Orchestration | Arranges and combines various processes in order to optimize output.
Transformation | Visual Redaction | Censors or obscures parts of an image or video, such as an individual's face.


Visual Guide to onboarding UI workflow
<A visual walkthrough of the onboarding process up to approval, use the existing UI until the new mocs are ready>
