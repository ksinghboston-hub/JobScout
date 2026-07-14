JobScout
AI-Powered Job Matching Application
developed by Kulbir Singh with AI assistance
README & User Guide

1.  Purpose
JobScout is a standalone, browser-based application that helps job seekers find remote and hybrid roles across North America that match their resume. It combines live job data from the JSearch API with optional AI-powered resume matching via Anthropic's Claude, all running in a single downloadable HTML file with no installation required.

Key goals of the application:
•	Search multiple job types simultaneously — Remote (North America), Hybrid Massachusetts, and Hybrid Connecticut — in a single click
•	Filter results to jobs posted within the last 3 days, 7 days, or 1 month
•	Score and rank each job against your resume using AI, surfacing the best matches first
•	Display clear match reasons so you understand exactly why a job is or is not a strong fit
•	Export matched results to CSV for tracking or sharing

Who is this for?
JobScout is designed for any job seeker in New England or targeting remote roles — no technical background required. If you can open a file in a browser and paste an API key, you can use this application.

2.  Requirements
2.1  Technical Requirements
JobScout has no installation requirements. The only things you need are:
•	A modern web browser — Chrome, Edge, or Firefox (Chrome/Edge recommended)
•	An internet connection (to call the job search and AI APIs)
•	The jobscout.html file saved anywhere on your computer

2.2  API Key Requirements

API Key	Required?	What it does	Cost
JSearch	✅ Required	Fetches live job listings from across the web	Free tier: 200 req/month
Anthropic Claude	⚡ Optional	Scores each job 0–100% against your resume with reasons	~$0.06 per search run

Note
Without the Anthropic key, the app still works — it fetches and displays all matching jobs. You just won't see AI match scores or reasons. The Anthropic key is only needed if you want ranked, scored results.

3.  Technologies Used

Technology	Category	Purpose
HTML5	Structure	Single-file app layout and user interface
CSS3 / CSS Variables	Styling	Dark-theme design, responsive layout, animations
Vanilla JavaScript	Programming	All app logic — no frameworks or build tools needed
Fetch API	Browser built-in	Makes HTTP calls to JSearch and Anthropic APIs
localStorage	Browser built-in	Persists API keys locally between sessions
Google Fonts	Typography	DM Sans, DM Mono, DM Serif Display fonts

Why no frameworks?  JobScout is intentionally built with plain HTML, CSS, and JavaScript — no React, no npm, no build step. This means you can open it directly as a file in any browser without installing anything. It also makes the code easy to read and extend.

4.  APIs Used
4.1  JSearch API (via RapidAPI)
Purpose:  Fetches live job listings from Google Jobs, LinkedIn, Indeed, and other sources.
Provider:  OpenWeb Ninja via RapidAPI
Endpoint:  https://jsearch.p.rapidapi.com/search
Sign up:  rapidapi.com → JSearch



4.2  Anthropic Claude API
Purpose:  Scores each job listing against your resume, returns a 0–100 match score and 2–3 specific reasons.
Provider:  Anthropic
Endpoint:  https://api.anthropic.com/v1/messages
Model used:  claude-sonnet-4-20250514
Sign up:  console.anthropic.com

What the AI receives per search run:
•	Your resume text (up to 2,500 characters)
•	Up to 20 job listings with title, company, and first 400 characters of description
•	Instructions to return a JSON array of {index, score, reasons} for each job

Privacy Note
Your resume text and job descriptions are sent directly from your browser to Anthropic's API. Nothing passes through any intermediate server. Anthropic's standard API data policies apply. Keys are stored only in your browser's localStorage and never transmitted to any third party.

5.  API Costs
5.1  JSearch (RapidAPI) Pricing

Plan	Monthly Price	Requests/Month	Best for
Free	$0	200	Testing, occasional use
Pro	$25	10,000	Daily searching (recommended)
Ultra	$75	50,000	Power users
Pay-as-you-go	—	Unlimited	$0.005 per request

For casual daily use:  The Free tier (200 requests/month) is sufficient for testing. For regular daily searching, the Pro plan at $25/month covers ~10,000 requests — far more than needed. Each search run uses 2–3 requests (one per location filter).

\
5.2  Anthropic API Pricing

Cost type	Rate	Per search run
Input tokens (resume + jobs)	$3.00 per 1M tokens	~11,000 tokens → ~$0.033
Output tokens (scores + reasons)	$15.00 per 1M tokens	~2,000 tokens → ~$0.030
Total per search run		~$0.06

Usage scenario	Estimated monthly cost
1 search per day for a month (30 runs)	~$1.80
3 searches per day for a month (90 runs)	~$5.40
$5 credit (starting credit)	~80 searches
$10 credit	~166 searches

Tip — Set a Spend Limit
Go to console.anthropic.com → Settings → Limits and set a monthly spend cap (e.g. $5 or $10). The API stops once the cap is reached, so you can never be charged more than you expect.

6.  How to Use the Application
6.1  First-Time Setup (2 minutes)

Step 1 — Get your JSearch API key (free)
1.  Go to rapidapi.com/letscrape-6bRBa3QguO5/api/jsearch
2.  Click Sign Up and create a free RapidAPI account
3.  Once logged in, click Subscribe to Test on the JSearch page
4.  Choose the Free plan (no credit card required)
5.  Copy your API key from the Code Snippets panel — it is a long string of letters and numbers

Step 2 — Get your Anthropic API key (optional, ~$5)
1.  Go to console.anthropic.com and create an account
2.  Navigate to Settings → API Keys → Create Key
3.  Give it a name like "JobScout" and copy the key — it starts with sk-ant-...
4.  Add $5 credit at console.anthropic.com/settings/billing
5.  Optionally, set a spend limit at console.anthropic.com/settings/limits

Step 3 — Open the app and complete setup
1.  Double-click jobscout.html — it opens in your default browser
2.  A setup wizard appears automatically on first open
3.  Paste your JSearch key in Step 1 of the wizard
4.  Paste your Anthropic key in Step 2 (or leave blank to skip AI matching)
5.  Click Save keys & start searching →
6.  Your keys are saved in your browser — you will not need to enter them again

Keys are saved locally
Both API keys are stored in your browser's localStorage. They never leave your computer except to go directly to the respective APIs. If you use a different browser, or move the HTML file to a different folder, you will need to re-enter them once.

6.2  Running a Search

Configure your filters (sidebar, left side)
•	Work type & location — tick/untick any combination of Remote, Hybrid MA, and Hybrid CT
•	Posted within — choose Last 3 days, Last 7 days, or Last month
•	Job keywords — type the role you are looking for, e.g. "data engineer" or "UX designer". Use the quick presets dropdown to pick common roles

Add your resume
•	Click the upload zone and select a .txt or .pdf file, or drag and drop it onto the zone
•	Alternatively, paste your resume text directly into the text box below the upload zone
•	Your resume is only used for AI scoring — if you did not enter an Anthropic key, this field is optional

Run the search
•	Click Find matching jobs
•	The app searches all selected locations simultaneously and deduplicates results
•	If AI matching is enabled, Claude scores each job and filters out poor matches (under 30%)
•	Results appear sorted by Best match (or Newest first — toggle in the top right)

Review results
•	Each card shows the job title, company, location tag (Remote / Hybrid), match score %, and posting date
•	Click any card to open the detail panel on the right — shows full description, match score bar, specific reasons, salary if listed, and a direct Apply button
•	Click Apply ↗ on any card or in the detail panel to open the company's application page
•	Press Escape to close the detail panel

Export results
•	After a search, an Export CSV button appears in the top header
•	Click it to download a spreadsheet with all matched jobs including title, company, location, match score, salary, and apply link

6.3  Updating Your API Keys
If you need to change or add an API key at any time:
1.  Click the ⚙ API Keys button in the top-right header
2.  The setup wizard reopens with your current keys pre-filled
3.  Update either key and click Save keys & start searching →

6.4  Adding New Location Filters
JobScout is designed to be extendable. To add a new state — for example, Rhode Island:
1.  Open jobscout.html in any text editor (Notepad, VS Code, TextEdit)
2.  Find the comment <!-- ADD NEW LOCATIONS HERE: --> in the HTML
3.  Uncomment or copy one of the existing location chip blocks and change the state name and key
4.  Find the comment // ADD NEW LOCATIONS HERE: in the JavaScript
5.  Add a matching entry with the same key string and appropriate query/location values
6.  Save the file and refresh the browser — the new filter appears immediately

No coding experience needed
Each extension point is marked with a clear comment. All you need to do is copy an existing block, change two values, and save. If you are unsure, ask Claude in the chat to help you add a specific state.

7.  Troubleshooting

Issue	Solution
"Failed to fetch"	Check your JSearch API key is correct and that you have an active free plan subscription on RapidAPI. The key must be pasted exactly with no spaces.
No jobs found	Try broader keywords (e.g. "engineer" instead of "senior backend engineer"), a wider date range, or confirm your API plan has remaining requests.
AI matching not working	Confirm your Anthropic API key starts with sk-ant- and that you have added credit at console.anthropic.com/settings/billing.
Keys not remembered	Make sure you saved via the setup wizard (not just typed in). Keys save to the browser's localStorage — they are tied to the browser and file location.
App looks broken	Try Chrome or Edge. Some browsers limit local file access. If the font does not load, check your internet connection (fonts come from Google Fonts).
Match scores missing	No Anthropic key is set. Click ⚙ API Keys to add one, or leave it blank to show all jobs unscored.

8.  Quick Reference

Action	How
Open app	Double-click jobscout.html in any folder
First-time setup	Setup wizard opens automatically — paste keys and click Save
Change API keys	Click ⚙ API Keys button in top header
Run a search	Set filters, paste resume, click Find matching jobs
View job detail	Click any job card
Close detail panel	Click ✕ or press Escape
Apply to a job	Click Apply ↗ on the card or in the detail panel
Export to spreadsheet	Click ⬇ Export CSV in the header after searching
Sort by newest	Click Newest first toggle above results
Add a new state	Edit HTML — find ADD NEW LOCATIONS HERE comments
Monitor API costs	console.anthropic.com/settings/usage
Set a spend cap	console.anthropic.com/settings/limits


JobScout is a personal-use tool. API costs are the responsibility of the user.
Built with HTML · JavaScript · JSearch API · Anthropic Claude API

