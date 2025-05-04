# Splunk-HTTP-Log-Analysis

# 🎯 Objective
- **Learn how to ingest and analyze HTTP logs using Splunk**
- **Detect client errors, server errors, and suspicious web activity.**
- **Identify large file transfers and suspicious URI access attempts.**

# 🖥️ Lab Setup
- **✅ Splunk: Already installed and accessible.**
- **✅ Data Source: JSON-formatted Zeek-style HTTP logs.**
- **🌐 Log File: Download and upload to Splunk using the steps below.**
      https://raw.githubusercontent.com/0xrajneesh/30-Days-SOC-Challenge-Beginner/refs/heads/main/http_logs.json

# ⚙️ Steps to Upload HTTP Log into Splunk
- **Go to Splunk Web → Settings > Add Data.**
![Ubuntu - VMware Workstation 16 Player (Non-commercial use only) 02-05-2025 11_17_48](https://github.com/user-attachments/assets/600cac41-7259-4490-8c44-61a471ee7b79)
- **Choose Upload and select synthetic_zeek_http.json**
![30-Days-SOC-Challenge-Beginner_Challenge#4_Day#18-Splunk Basics_ SSH Log Analysis md at main · 0xrajneesh_30-Days-SOC-Challenge-Beginner - Google Chrome 03-05-2025 08_45_52](https://github.com/user-attachments/assets/53bc100f-72a3-4966-9634-aa9d58743b7c)
- **Set Source type: json or create a new one zeek:http**
![30-Days-SOC-Challenge-Beginner_Challenge#4_Day#18-Splunk Basics_ SSH Log Analysis md at main · 0xrajneesh_30-Days-SOC-Challenge-Beginner - Google Chrome 03-05-2025 08_46_44](https://github.com/user-attachments/assets/93e6a215-c00e-4822-86b6-1d70dbbd5cfe)
- **Choose main or create a new index like http_lab**
- **Finish the upload and confirm indexing.**
![30-Days-SOC-Challenge-Beginner_Challenge#4_Day#18-Splunk Basics_ SSH Log Analysis md at main · 0xrajneesh_30-Days-SOC-Challenge-Beginner - Google Chrome 03-05-2025 08_46_54](https://github.com/user-attachments/assets/adcf9264-47d5-4d4c-ae94-6604d366b7e1)

# 🔍 Lab Tasks
Use SPL queries to complete the following analysis:
## ✅ Task 1: Find the top 10 endpoints generating web traffic
- **index=http_lab sourcetype="json"
| stats count by "id.orig_h"
| sort -count
| head 10**
![Search _ Splunk 9 4 2 - Google Chrome 03-05-2025 09_29_53](https://github.com/user-attachments/assets/eecc0fe4-1634-40af-9b70-f4b7621b5bbe)

## ✅Task 2: Count the number of server errors (5xx) observed.
- **index=http_lab sourcetype="json" status_code>=500 status_code<600
| stats count as server_errors**
![Search _ Splunk 9 4 2 - Google Chrome 03-05-2025 09_34_50](https://github.com/user-attachments/assets/bd83c985-5b53-4859-ae9f-408def1c500d)

## ✅Task 3: Identify User-Agents associated with possible scripted attacks.
- **index=http_lab sourcetype="json" user_agent IN ("sqlmap/1.5.1", "curl/7.68.0", "python-requests/2.25.1", "botnet-checker/1.0")
| stats count by user_agent**
![Search _ Splunk 9 4 2 - Google Chrome 03-05-2025 09_43_09](https://github.com/user-attachments/assets/beb74803-2628-42ed-a41b-1c863362a8be)

## ✅Task 4: Find large file transfers (greater than 500 KB)
- **index=http_lab sourcetype="json" resp_body_len>500000
| table ts "id.orig_h" "id.resp_h" uri resp_body_len
| sort -resp_body_len**
![Search _ Splunk 9 4 2 - Google Chrome 03-05-2025 09_44_02](https://github.com/user-attachments/assets/7d755102-f4ec-44ad-aca9-c18f9e1a679a)

## ✅Task 5: Identify top user agents
- **index=http_lab sourcetype="json" | top user_agent**
![Search _ Splunk 9 4 2 - Google Chrome 03-05-2025 09_53_37](https://github.com/user-attachments/assets/8ccb259a-b2d0-4853-9a12-d98692fc39ac)

# Conclusion
- **Learned how to analyze the HTTP traffic in splunk SIEM , Analyzed Count of number of server errors (5xx) observed ,  Find the top 10 endpoints generating web traffic etc . Got hands on knowledge about http protocol and its response code etc . Got hands on of Splunk SIEM.**






















