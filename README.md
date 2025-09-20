# Synapse-ATS: AI-Powered Resume & Job Matcher

**Synapse-ATS** is an intelligent system designed to automate the recruitment pipeline by matching candidate resumes with job descriptions. It leverages the power of Google's **Gemini family of models** for deep semantic understanding, parsing, and scoring, ensuring a high-quality match between talent and opportunity.

-----

## System Architecture

The high-level architecture visualizes the flow of data from ingestion to the final scoring and storage.

```mermaid
graph TD
    subgraph User & External Inputs
        Candidate[<i class='fa fa-user'></i> Candidate]
        JobPlatforms[<i class='fa fa-building'></i> Job Platforms]
    end

    subgraph Resume Matching System
        subgraph Ingestion & API Layer
            UI_API[User Interface / API Gateway]
            JobScraper[Job Scraper]
        end

        subgraph AI Processing Core
            ResumeProcessor[1. Resume Processor]
            MatchingScoringEngine[3. Matching & Scoring Engine]
        end

        subgraph Data Storage
            RDBMS[<i class='fa fa-database'></i> Relational Database<br>]
        end

        subgraph External AI Service
            GeminiAPI[<i class='fa fa-robot'></i> Gemini Family Models API]
        end
    end

    %% Data Flow & Interactions
    Candidate -- Uploads Resume --> UI_API
    UI_API --> ResumeProcessor
    JobScraper -- Scrapes Job Postings --> JobPlatforms
    JobScraper --> RDBMS

    ResumeProcessor -- "For ATS Keyword Segregation" --> GeminiAPI
    GeminiAPI -- Returns Structured Data --> ResumeProcessor
    ResumeProcessor -- 2. Stores Processed Data --> RDBMS

    MatchingScoringEngine -- Fetches Resumes & Jobs --> RDBMS
    MatchingScoringEngine -- "For Match Algorithm" --> GeminiAPI
    GeminiAPI -- Returns Match Analysis --> MatchingScoringEngine
    MatchingScoringEngine -- 4. Updates DB with Score --> RDBMS
```

-----

## Features

  * **AI-Powered Resume Parsing:** Extracts skills, experience, and education using the Gemini API.
  * **Automated Job Scraping:** Gathers job descriptions from various online platforms.
  * **Intelligent Matching & Scoring:** Calculates a compatibility score between each resume and job posting.
  * **RESTful API:** Provides endpoints for uploading resumes and retrieving matched results.

-----

## Tech Stack

  * **Backend:** Python (FastAPI)
  * **Database:** PostgreSQL
  * **AI Model:** Google Gemini API

-----
