# automatic-tiktok-quality-analysis-tool

The tool executes the following steps:
1.  **Downloads Videos:** Uses `yt-dlp` to download both the reference and user-submitted TikTok videos.
2.  **Transcribes Audio:** Employs OpenAI's `whisper` model to generate a transcript for both videos.
3.  **Uploads to Cloud:** Moves the video files to a Google Cloud Storage bucket to be accessible by the AI model.
4.  **Multimodal Analysis:** Sends the video files and transcripts to the Gemini Pro Vision model via the Vertex AI SDK.
5.  **Generates Report:** The model analyzes the videos based on a detailed rubric and produces a score, qualitative feedback, and a final recommendation.

# Setup Instructions 
1) Change "PROJECT_ID", "LOCATION", and "BUCKET_NAME" to your own Gemini AI Project and Google Cloud Bucket.
2) Run each cell in the jyupter notebook one by one in order except the last cell.
3) In the last cell replace the reference_url string to the link of the TikTok video you want to use as a reference.
4) Then do the same for user_url (this is the video you want to compare the reference to)

# Scoring Logic
This is the current scoring logic (can be changed accordingly):

    Given the brand reference video description (transcript of the reference video)
    And the uploaded video description (transcript of the user uploaded video)
    Rate the uploaded video's quality from 0 to 100 based on tone, clarity, and brand consistency 
    using the reference video provided as the ideal tone/manner.
    Show the evaluated score and then give feedback as a list of points (e.g., “Lighting too dark”, “Brand name not mentioned”)
    Then provide a recommendation to either pass, re-shoot, or manual review the video.
    """

# Limitations
 - Currently the program requires my Google account authentication in order for the tool to to work as it uses my paid Gemini Pro Vision and my Google Cloud.
 - Since the scoring is made by a generative AI Model, there may be slight variations between runs, but not enough to change results.
 - Longer TikTok videos take longer to analyze.
  
# Next steps 
 - Develop a better pipeline so multiple user-uploaded videos can be fed into the tool and analyzed.
 - Allow for the tool to read and use .csv files with TikTok links in its analyzation.  
 - Improve scoring logic to make it more robust.
