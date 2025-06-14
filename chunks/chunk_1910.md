### Post 8
**Post URL**: /t/regarding-project1-for-file-not-detecting-after-sending-post-request/167172/8
- **ID**: 595104
- **Author**: SAKSHI PATHAK (Sakshi6479)
- **Created At**: 2025-02-14T17:48:35.347Z
- **Reply To**: Post 7 (Saransh Saini, Saransh_Saini)
- **Content**:  
  sir i have tried that by putting by doing this
<pre><code class="lang-auto">import os
from dotenv import load_dotenv
import json
import requests
from dateutil import parser as date_parser
from sklearn.metrics.pairwise import cosine_similarity
from fastapi import FastAPI, HTTPException
from fastapi.middleware.cors import CORSMiddleware
import pandas as pd
from fastapi.responses import StreamingResponse, JSONResponse
from typing import Dict, Any, List
import subprocess
import datetime
from pathlib import Path
import sqlite3
import base64
import mimetypes
import numpy as np


app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["GET", "POST"],
    allow_headers=["*"],
)

#AIPROXY_TOKEN = os.getenv("AIPROXY_TOKEN")
AIPROXY_TOKEN = os.getenv("AIPROXY_TOKEN")
def cakebake(no_people: int, flavor: str):
    return {"message": f"Making a {flavor} cake for {no_people} people"}

bakecake = {
    "type": "function",
    "function": {
        "name": "cakebake",
        "description": "Make a cake for all iitm students contain its emailids",
        "parameters": {
            "type": "object",
            "properties": {
                "no_people": {
                    "type": "integer",
                    "description": "Number of people"
                },
                "flavor": {
                    "type": "string",
                    "description": "Flavor of the cake"
                }
            },
            "required": ["no_people", "flavor"],
            "additionalProperties": False
        },
        "strict": True
    }
}

def sort_contacts(contacts_file_path: str, output_file_path: str):
    try:
        contacts = pd.read_json(contacts_file_path)
        contacts.sort_values(["last_name", "first_name"]).to_json(output_file_path, orient="records")
        return {"message": f"Contacts sorted and saved to {output_file_path}"}
    except Exception as e:
        return {"error": f"Failed to sort contacts: {str(e)}"}

tools = [bakecake, a1_tool, a2_tool, a3_tool, a4_tool, a5_tool, a6_tool, a7_tool, a8_tool, a9_tool, a10_tool]



def query_gpt(user_input: str, tools: list[dict] = tools) -&gt; dict[str, Any]:
    response = requests.post(
        url="https://aiproxy.sanand.workers.dev/openai/v1/chat/completions",
        headers={
            "Content-Type": "application/json",
            "Authorization": f"Bearer {AIPROXY_TOKEN}"
        },
        json={
            "model": "gpt-4o-mini",
            "messages": [
                {
                    "role": "system",
                    "content": """
                        Whenever you receive a system directory location, always make it into a realtive path, for example adding a . before it would make it relative path, rest is on you to manage, I just want the relative path"""
                },
                {
                    "role": "user",
                    "content": user_input
                }
            ],
            "tools": tools,
            "tool_choice": "auto"
        }
    )
    return response.json()

@app.get("/")
def home():
    return {"Hello": "World"}

@app.get("/read")
def read_file(path: str):
    try:
        with open(path, "r") as f:
            return f.read()
    except Exception as e:
        raise HTTPException(status_code=404, detail="File does not exist")

@app.post("/run")
async def run(task: str):
    query = query_gpt(task)
    print(query)  # Print the full response to inspect it.
    
    if 'choices' not in query:
        raise HTTPException(status_code=500, detail="Invalid response format from GPT API")
    
    try:
        tool_calls = query['choices'][0]['message'].get('tool_calls', [])
        if tool_calls:
            func_name = tool_calls[0]['function']['name']
            args = json.loads(tool_calls[0]['function']['arguments'])
            
            # Map function names to their respective functions
            function_map = {
                "cakebake": cakebake,
                "install_uv_and_run_datagen": install_uv_and_run_datagen,
                "format_markdown_file": format_markdown_file,
                "count_wednesdays": count_wednesdays,
                "sort_contacts": sort_contacts,
                "extract_recent_logs": extract_recent_logs,
                "create_markdown_index": create_markdown_index,
                "extract_sender_email": extract_sender_email,
                "extract_credit_card_number": extract_credit_card_number,
                "find_similar_comments": find_similar_comments,
                "calculate_gold_ticket_sales": calculate_gold_ticket_sales,
            }
            
            if func_name in function_map:
                output = function_map[func_name](**args)
            else:
                raise HTTPException(status_code=500, detail="Unknown function called")
        else:
            raise HTTPException(status_code=500, detail="No function call found in response")
    except KeyError as e:
        raise HTTPException(status_code=500, detail=f"KeyError: Missing key in response - {str(e)}")
    except Exception as e:
        raise HTTPException(status_code=500, detail=f"Error processing the request: {str(e)}")
    
    return output

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
</code></pre>
and also i am sending postman request as <a href="http://localhost:8000/run?task=The" rel="noopener nofollow ugc">http://localhost:8000/run?task=The</a> file ./data/dates.txt contains a list of dates, one per line. Count the number of Wednesdays in the list, and write just the number to ./data/dates-wednesdays.txt<br>
do I need to use dockerfile for this? i am still getting the same error as<br>
<div class="lightbox-wrapper"><a class="lightbox" href="https://europe1.discourse-cdn.com/flex013/uploads/iitm/original/3X/3/c/3c786f00a8e4f37db2c31ff21edffb3e68396b59.png" data-download-href="/uploads/short-url/8CWFUFCn1rd2HZakNRDmzHnnKmR.png?dl=1" title="Screenshot 2025-02-14 231752" rel="noopener nofollow ugc"><img src="https://europe1.discourse-cdn.com/flex013/uploads/iitm/optimized/3X/3/c/3c786f00a8e4f37db2c31ff21edffb3e68396b59_2_690x411.png" alt="Screenshot 2025-02-14 231752" data-base62-sha1="8CWFUFCn1rd2HZakNRDmzHnnKmR" width="690" height="411" srcset="https://europe1.discourse-cdn.com/flex013/uploads/iitm/optimized/3X/3/c/3c786f00a8e4f37db2c31ff21edffb3e68396b59_2_690x411.png, https://europe1.discourse-cdn.com/flex013/uploads/iitm/optimized/3X/3/c/3c786f00a8e4f37db2c31ff21edffb3e68396b59_2_1035x616.png 1.5x, https://europe1.discourse-cdn.com/flex013/uploads/iitm/optimized/3X/3/c/3c786f00a8e4f37db2c31ff21edffb3e68396b59_2_1380x822.png 2x" data-dominant-color="272828"><div class="meta"><svg class="fa d-icon d-icon-far-image svg-icon" aria-hidden="true"><use href="#far-image"></use></svg><span class="filename">Screenshot 2025-02-14 231752</span><span class="informations">1786×1065 74.8 KB</span><svg class="fa d-icon d-icon-discourse-expand svg-icon" aria-hidden="true"><use href="#discourse-expand"></use></svg></div></a></div><br>
<a class="mention" href="/u/carlton">@carlton</a> , <a class="mention" href="/u/saransh_saini">@Saransh_Saini</a> , <a class="mention" href="/u/jivraj">@Jivraj</a>
- **Reactions**: None
- **Post Number**: 8

