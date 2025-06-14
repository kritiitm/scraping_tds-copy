### Post 210
**Post URL**: /t/project-2-tds-solver-discussion-thread/169029/210
- **ID**: 613689
- **Author**: Shivaditya Bhattacharya (22f3000819)
- **Created At**: 2025-03-30T23:47:44.092Z
- **Content**:  
  <a class="mention" href="/u/saransh_saini">@Saransh_Saini</a> <a class="mention" href="/u/jivraj">@Jivraj</a> <a class="mention" href="/u/carlton">@carlton</a><br>
Sir, I have an issue in GA5 Q3
What is the number of successful GET requests for pages under <strong>/telugu/</strong> from <strong>11:00</strong> until before <strong>20:00</strong> on Mondays?
For this, I have used two python scripts to get the answer, one written completely by me and another from someone else’s solution; both give the same answer - <strong>2698</strong>
However, the portal says it’s incorrect. No modifications resulting in different answer are being accepted either and the modifications themselves seem to break the bounds of the question.
Please check the scripts and tell me where I am going wrong.
My script:
<pre><code class="lang-auto">import subprocess
from datetime import datetime

def isDay(dtobj, day):
  return dtobj.weekday() == day

def isTime(dtobj, l, u):
  return l &lt;= dtobj.hour &lt; u

step1 = subprocess.run("cat data | grep -i 'GET /telugu/'", capture_output=True, shell=True, text=True)
subprocess.run("rm -f forstep2.txt", shell=True)
with open('forstep2.txt', 'a') as f:
  for line in step1.stdout.splitlines():
    try:
      status = int(line.split()[8])
    except Exception as e:
      status = 400
    if 200 &lt;= status &lt; 300:
      f.write(line + '\n')
step2 = subprocess.run("cat forstep2.txt | cut -d ' ' -f4", capture_output=True, shell=True, text=True)
count = 0
for line in step2.stdout.splitlines():
  log_datetime = datetime.strptime(line.strip('['), "%d/%b/%Y:%H:%M:%S")
  if(isDay(log_datetime, 0) and isTime(log_datetime, 11, 20)):
    count += 1

count
</code></pre>
I had extracted and uploaded the <code>data</code> after extraction using gzip into colab and then executed the script.
The other script:
<pre><code class="lang-auto">import pandas as pd
import gzip
import re
import os
from datetime import datetime
import hashlib
from google.colab import files

# Function to compute SHA-256 hash
def compute_hash(text):
    return hashlib.sha256(text.encode()).hexdigest()

# Function to parse Apache log entries
def parse_log_line(line):
    log_pattern = (r'^(\S+) (\S+) (\S+) \[(.*?)\] "(\S+) (.*?) (\S+)" (\d+) (\S+) "(.*?)" "(.*?)" (\S+) (\S+)$')
    match = re.match(log_pattern, line)
    if match:
        return {
            "ip": match.group(1),
            "time": match.group(4),
            "method": match.group(5),
            "url": match.group(6),
            "protocol": match.group(7),
            "status": int(match.group(8)),
            "size": match.group(9),
            "referer": match.group(10),
            "user_agent": match.group(11),
            "vhost": match.group(12),
            "server": match.group(13)
        }
    return None

# Upload file
uploaded = files.upload()
file_path = list(uploaded.keys())[0]  # Get uploaded file name

# Load and parse the log file
def load_logs(file_path):
    if not os.path.exists(file_path):
        print(f"Error: File '{file_path}' not found.")
        return pd.DataFrame()

    parsed_logs = []
    with gzip.open(file_path, 'rt', encoding='utf-8') as f:
        for line in f:
            parsed_entry = parse_log_line(line)
            if parsed_entry:
                parsed_logs.append(parsed_entry)
    return pd.DataFrame(parsed_logs)

# Convert time format
def convert_time(timestamp):
    return datetime.strptime(timestamp, "%d/%b/%Y:%H:%M:%S %z")

df = load_logs(file_path)

if not df.empty:
    df["datetime"] = df["time"].apply(convert_time)
    df["day_of_week"] = df["datetime"].dt.strftime('%A')
    df["hour"] = df["datetime"].dt.hour

    # Filter conditions
    filtered_df = df[
        (df["method"] == "GET") &amp;
        (df["url"].str.startswith("/telugu/")) &amp;
        (df["status"] &gt;= 200) &amp; (df["status"] &lt; 300) &amp;
        (df["day_of_week"] == "Monday") &amp;
        (df["hour"] &gt;= 11) &amp;
        (df["hour"] &lt; 20)
    ]

    # Compute hash of the result
    result_hash = compute_hash(str(len(filtered_df)))

    # Output the count and hash
    print("Successful GET requests for /telugu/ on Mondays (11:00-7:59 AM):", len(filtered_df))
else:
    print("No log data available for processing.")
</code></pre>
Both give the same output: 2698. Please help me identify the error, if any.
- **Reactions**: None
- **Post Number**: 210

