🚀 Enhanced CrewAI Job Search Agent System
An AI-powered job search automation system that uses multiple specialized AI agents to provide personalized career guidance based on your resume and target job preferences.
🎯 What This System Does
Instead of manually searching for jobs and crafting applications, this system deploys 4 specialized AI agents that work together like a professional career consulting team:

🔍 Job Search Specialist: Finds relevant job openings using real APIs
📚 Skills Development Advisor: Analyzes your background vs job requirements
🎭 Interview Preparation Expert: Creates personalized interview strategies
💼 Career Strategy Advisor: Optimizes your resume, LinkedIn, and networking approach

Key Innovation: The system analyzes your actual resume to provide contextualized recommendations instead of generic advice.


📋 Table of Contents
Features
Installation
Configuration
Project Structure
How It Works
Usage Guide
Code Architecture
Sample Outputs
Troubleshooting
API Requirements


✨ Features
🎯 Personalized Analysis
Resume parsing: Extracts skills, experience, and background from your PDF
Contextual recommendations: All advice tailored to your specific profile
Gap analysis: Compares your skills with job requirements
Career progression mapping: Understands your professional journey
🔍 Real Job Market Data
Live job search: Uses Adzuna API for current job listings
Detailed job analysis: Salary, requirements, company info
Market insights: Trending skills and demand patterns
🤖 AI Agent Collaboration
Hierarchical workflow: Agents build on each other's work
Specialized expertise: Each agent has focused knowledge domain
Comprehensive output: Complete career strategy in one report
🛡️ Smart Fallbacks
Works with or without resume: Graceful degradation to general advice
Multiple PDF parsers: Handles various PDF formats
Error handling: Clear messages and alternative approaches


🚀 Installation
Prerequisites
Python 3.8 or higher
OpenAI API account
Adzuna API account (free tier available)
Step 1: Clone and Setup
# Clone or download the project

git clone <your-repo-url>

cd crewai-job-search

# Create virtual environment (recommended)

python -m venv venv

source venv/bin/activate  # On Windows: venv\Scripts\activate
Step 2: Install Dependencies
pip install crewai langchain langchain-openai requests python-dotenv PyPDF2 pdfplumber
Step 3: API Key Setup
Create a .env file in your project directory:

# OpenAI API Key - Get from https://platform.openai.com/account/api-keys

OPENAI_API_KEY=your_openai_api_key_here

# Adzuna Job Search API - Get from https://developer.adzuna.com/

ADZUNA_APP_ID=your_adzuna_app_id_here

ADZUNA_API_KEY=your_adzuna_api_key_here
Step 4: Add Your Resume
Place your resume PDF in the project directory:

cp /path/to/your/resume.pdf ./resume.pdf


⚙️ Configuration
API Keys Setup
🔑 OpenAI API Key:

Visit platform.openai.com
Create account or sign in
Navigate to "API Keys" section
Click "Create new secret key"
Copy the key to your .env file

🔑 Adzuna API Keys:

Visit developer.adzuna.com
Register for free developer account
Create a new application
Copy App ID and API Key to your .env file
Resume Requirements
Format: PDF only (not Word docs or images)
Type: Text-based PDFs (not scanned documents)
Name: Must be exactly resume.pdf
Location: Same directory as the Python script


📁 Project Structure
crewai-job-search/

├── .env                        # API keys (create this)

├── resume.pdf                  # Your resume (add this)

├── job_search_system.py        # Main application

├── task_output.txt            # Generated report (auto-created)

└── README.md                  # This file


🔄 How It Works
System Architecture Overview
graph TD

    A[Resume PDF] --> B[Resume Parser]

    C[Job Search Parameters] --> D[Job Search Agent]

    B --> E[AI Agent Context]

    D --> F[Job Listings]

    E --> G[Skills Development Agent]

    E --> H[Interview Prep Agent]

    E --> I[Career Strategy Agent]

    F --> G

    F --> H

    F --> I

    G --> J[Comprehensive Report]

    H --> J

    I --> J
Workflow Steps
📄 Resume Analysis: System parses your PDF and extracts professional background
🔍 Job Discovery: Searches live job APIs for relevant positions
🧠 AI Collaboration: 4 specialized agents analyze data in sequence
📊 Report Generation: Comprehensive career strategy document created
💾 Output Storage: Results saved to file for reference


🎮 Usage Guide
Basic Usage
Ensure setup is complete:

.env file with API keys
resume.pdf in project directory
Dependencies installed

Run the system:

python job_search_system.py

Customize search parameters (edit in main() function):

# Example usage - customize these parameters

role = "Senior Data Scientist"        # Target job title

location = "New York"                 # Geographic area

num_results = 5                       # Number of jobs to analyze
Advanced Usage
Custom Resume Path:

# If your resume is in a different location

job_search_system = EnhancedJobSearchAgentSystem(

    resume_path="/path/to/different/resume.pdf"

)

Programmatic Usage:

from job_search_system import EnhancedJobSearchAgentSystem

# Initialize system

system = EnhancedJobSearchAgentSystem(resume_path="resume.pdf")

# Run multiple searches

results = []

for role in ["Data Scientist", "ML Engineer", "Analytics Manager"]:

    result = system.search_jobs(role=role, location="San Francisco")

    results.append(result)
Expected Output
🔧 Enhanced Job Search System Setup:

✅ Loading configuration from .env file...

📄 Found resume file: resume.pdf

📄 Parsing resume from: resume.pdf

✅ Resume parsed and ready for analysis!

🚀 Starting PERSONALIZED job search for 'Senior Data Scientist' in 'New York'...

📄 Using resume content for personalized recommendations

📝 This process will:

   1. Search for relevant job openings

   2. Compare job requirements with your background

   3. Create personalized skill development plan

   4. Prepare customized interview strategies

   5. Generate targeted career optimization plan

   6. Provide actionable next steps

==================================================

[Agent execution details...]

==================================================

✅ Personalized job search analysis complete!

📄 Detailed results saved to 'task_output.txt'

🎯 All recommendations are tailored to your specific background!


🏗️ Code Architecture
Module Breakdown
1. ResumeAnalysisTools Class
class ResumeAnalysisTools:

    @tool("Resume Parser Tool")

    def parse_resume(file_path: str) -> str:

Purpose: Extracts text content from PDF resumes

Primary parser: pdfplumber (better text extraction)
Fallback parser: PyPDF2 (broader compatibility)
Error handling: Graceful degradation with helpful messages
2. JobSearchTools Class
class JobSearchTools:

    @tool("Job Search Tool") 

    def search_jobs(input_json: str) -> str:

Purpose: Interfaces with Adzuna API for live job data

Input validation: Ensures proper JSON format
API communication: Handles HTTP requests and responses
Data formatting: Structures job information for AI agents
Error handling: Manages API failures and rate limits
3. EnhancedJobSearchAgentSystem Class
Main orchestrator that coordinates the entire system:

3.1 Initialization (__init__)

def __init__(self, resume_path: str = None):

Validates API keys from .env file
Initializes OpenAI connection
Parses resume if provided
Sets up agents, tasks, and crew

3.2 Agent Setup (setup_agents) Creates 4 specialized AI agents with resume context:

🔍 Job Search Specialist

Role: Find relevant job opportunities
Tools: Job search API access
Context: Candidate's background for better matching

📚 Skills Development Advisor

Role: Personalized skill gap analysis
Context: Current skills vs job requirements
Output: Targeted learning recommendations

🎭 Interview Preparation Expert

Role: Customized interview coaching
Context: Specific background and career transitions
Output: Personalized questions and strategies

💼 Career Strategy Advisor

Role: Resume and networking optimization
Context: Current professional profile
Output: Specific improvement recommendations

3.3 Task Configuration (setup_tasks) Defines what each agent should accomplish:

Sequential execution: Later tasks build on earlier results
Context sharing: Agents can see previous agents' work
Personalization: All tasks use resume content for context
Expected outputs: Clear deliverables for each agent

3.4 Crew Management (setup_crew)

self.crew = Crew(

    agents=[...],

    tasks=[...], 

    process=Process.hierarchical,

    manager_llm=self.llm

)

Hierarchical process: Tasks execute in logical order
AI manager: Coordinates workflow and resolves conflicts
Verbose mode: Shows detailed progress information
4. Main Execution Flow
4.1 Job Search Method (search_jobs)

def search_jobs(self, role: str, location: str, num_results: int = 5):

Parameter configuration: Sets search criteria
Progress tracking: Shows workflow steps
Report generation: Creates comprehensive output file
Error handling: Manages execution failures

4.2 Main Function (main)

Environment validation: Checks API keys and file presence
System initialization: Creates agent system with resume
Example execution: Demonstrates usage with sample parameters
Error reporting: Provides helpful troubleshooting messages


📊 Sample Outputs
Without Resume (Generic)
Skills Development Recommendations:

- Learn Python programming basics

- Study machine learning fundamentals  

- Get familiar with SQL databases

- Practice data visualization
With Resume (Personalized)
=== Skills Development Advisor - Personalized Analysis ===

BACKGROUND ANALYSIS:

✅ Current Strengths (From Resume):

- Python programming (3+ years experience)

- SQL databases (Advanced level)

- Statistical analysis (MS Statistics degree)

- Project management (Led 5+ data projects)

🎯 PRIORITY SKILL GAPS (Target Jobs Analysis):

1. Deep Learning Frameworks

   - Current: Basic TensorFlow knowledge

   - Required: Advanced PyTorch, TensorFlow 2.0

   - Action: Complete Fast.ai course (8 weeks)

   

2. Cloud Platforms  

   - Current: Local development only

   - Required: AWS/GCP experience

   - Action: AWS Solutions Architect certification (4 weeks)

3. MLOps Pipeline

   - Current: Model building only  

   - Required: Docker, Kubernetes, CI/CD

   - Action: MLOps specialization course (6 weeks)

📈 PERSONALIZED LEARNING ROADMAP:

Week 1-4:  AWS Cloud certification

Week 5-12: Deep learning with Fast.ai  

Week 13-18: MLOps and deployment skills

💡 RESUME ENHANCEMENT:

- Add "TensorFlow" to your XYZ project description

- Quantify model performance improvements

- Include links to GitHub portfolio
Interview Preparation (Personalized)
=== Interview Preparation Expert - Customized Strategy ===

🎯 YOUR ELEVATOR PITCH:

"I'm a data scientist with a unique background combining 5 years of finance 

experience with advanced technical skills. My banking background gives me 

deep domain expertise in risk modeling, while my recent MS in Data Science 

provides cutting-edge technical knowledge..."

🔥 STRENGTH-BASED QUESTIONS & ANSWERS:

Q: "Tell me about your transition from finance to data science."

A: "My finance background actually accelerated my data science learning. 

I already understood business context and stakeholder needs. For example, 

in my capstone project, I built a credit risk model that improved accuracy 

by 15% because I understood both the technical and business requirements..."

Q: "How do you handle working with business stakeholders?"

A: "My finance experience taught me to translate technical concepts into 

business value. In my last project, I presented ML model results to the 

C-suite by focusing on ROI rather than technical metrics..."

⚠️ ADDRESSING POTENTIAL CONCERNS:

Q: "You're relatively new to programming. How do you ensure code quality?"

A: "While I'm newer to programming than some candidates, my systematic approach 

from finance helps me write clean, well-documented code. I also leverage 

code reviews and testing frameworks. Here's an example from my recent project..."

🎯 TECHNICAL QUESTIONS FOR YOUR BACKGROUND:

[Customized technical questions based on resume projects]


🔧 Troubleshooting
Common Issues & Solutions
❌ Problem: Resume file not found at: resume.pdf ✅ Solution:

Ensure file is named exactly resume.pdf
Check file is in same directory as Python script
Verify file is a PDF (not Word doc or image)

❌ Problem: Could not extract text from PDF ✅ Solution:

PDF might be image-based (scanned document)
Try converting to text-based PDF using online tools
Ensure PDF uses standard fonts

❌ Problem: Missing required environment variables ✅ Solution:

Create .env file in project directory
Add all required API keys
Restart terminal/IDE after creating .env file

❌ Problem: HTTP Error from job search API ✅ Solution:

Check Adzuna API keys are correct
Verify internet connection
Try reducing num_results parameter
Check API rate limits

❌ Problem: Generic recommendations despite having resume ✅ Solution:

Check console for resume parsing success message
Ensure resume has clear text (not images)
Try different PDF format/export settings
Debug Mode
Enable verbose logging by setting verbose=True in agent definitions to see detailed execution steps.


🔑 API Requirements
OpenAI API
Purpose: Powers AI agents and natural language processing
Cost: Pay-per-token (typically $1-5 per job search)
Limits: Rate limits apply (usually sufficient for personal use)
Model: Uses GPT-4 Turbo for best results
Adzuna Job Search API
Purpose: Provides live job market data
Cost: Free tier available (1000+ requests/month)
Coverage: US, UK, and other major markets
Limits: Rate limiting (1 request/second on free tier)
Usage Optimization
Batch searches: Analyze multiple similar roles together
Cache results: Save outputs to avoid re-running same searches
Monitor costs: Track OpenAI API usage in dashboard


🎯 Best Practices
Resume Optimization for AI Analysis
Use Standard Section Headers:

✅ Good: "WORK EXPERIENCE", "SKILLS", "EDUCATION" 

❌ Poor: "My Journey", "What I Know", "Learning"

Include Specific Technologies:

✅ Good: "Python, TensorFlow, scikit-learn, AWS, PostgreSQL"

❌ Poor: "Programming languages and databases"

Quantify Achievements:

✅ Good: "Improved model accuracy by 15% using ensemble methods"

❌ Poor: "Worked on machine learning models"
Search Strategy
Start with broader role terms, then get specific
Try different location variations (city, state, region)
Adjust num_results based on market size
Run searches for related roles to compare opportunities
Output Analysis
Focus on skills that appear across multiple job listings
Prioritize learning recommendations with shorter timelines
Use interview preparation for actual interview practice
Implement career strategy suggestions systematically


🤝 Contributing
Contributions welcome! Areas for improvement:

Additional job search APIs (Indeed, LinkedIn, etc.)
Resume format support (Word docs, text files)
More specialized agent roles (salary negotiator, etc.)
Integration with job application tracking
Advanced resume parsing (work history timeline analysis)


📄 License
This project is licensed under the MIT License - see the LICENSE file for details.


🙋‍♂️ Support
For issues or questions:

Check the troubleshooting section above
Verify all dependencies are installed correctly
Ensure API keys are valid and have sufficient credits
Check that resume.pdf is readable and text-based

Remember: The system provides the most value when it has your actual resume to analyze. Generic mode is available as a fallback, but personalized recommendations based on your background are significantly more actionable and relevant!

Env File Template (store the below info in a .env file)

# CrewAI Job Search Agent Configuration
# Copy this template to a .env file in your project directory

# OpenAI API Key - Get from https://platform.openai.com/account/api-keys
OPENAI_API_KEY=your_openai_api_key_here

# Adzuna Job Search API - Get from https://developer.adzuna.com/
ADZUNA_APP_ID=your_adzuna_app_id_here
ADZUNA_API_KEY=your_adzuna_api_key_here

# Optional: Customize default search parameters
# DEFAULT_ROLE=Senior Data Scientist
# DEFAULT_LOCATION=New York
# DEFAULT_NUM_RESULTS=5



