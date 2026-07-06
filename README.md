# Live_weather_dashboard
A Python-based command-line interface that fetches real-time global weather data from the OpenWeatherMap API using requests. It parses JSON payloads, displays a cleanly formatted terminal dashboard, and uses a Pandas pipeline to log and append structured search history to a local CSV file.


        ​📌 Table of Contents


 ​1. Project Overview

 ​2. Key Features

 ​3. Architecture & Data Flow

 ​4. Tech Stack & Prerequisites

 ​5. Installation & Setup

 ​5.a Cloning the Repository

 ​5.b Environment Configuration

 ​6. Execution & Usage

​7. Data Schema (CSV Log)

​8. Future Enhancements

​9. License

       PROJECT OVERVIEW

The Live Weather Dashboard (CLI) is a lightweight, production-ready Python command-line application engineered to showcase the end-to-end integration of public REST APIs, structured data processing pipelines, and local data persistence.

​🎯 Objective

​The primary goal of this project is to bridge the gap between live cloud data and local analytical storage. Instead of just displaying fleeting real-time data to a user, this application serves as a functional data pipeline that captures, normalizes, and logs historical inquiries for downstream analysis.

​🔄 How It Works

​Data Ingestion: The application accepts user input (a city name) via the terminal and constructs a secure HTTP request to the OpenWeatherMap API endpoints.

​Data Transformation & Parsing: Upon receiving a raw JSON payload, the script extracts key meteorological metrics (such as temperature, humidity, wind speed, and weather conditions) and standardizes units of measurement.

​User Interface (UI): The parsed metrics are instantly rendered into a clean, human-readable terminal dashboard layout using robust formatting techniques.

​Pandas Pipeline & Storage: Simultaneously, the application converts the data point into a single-row matrix and utilizes a Pandas DataFrame pipeline to append the data. If the historical database (weather_history.csv) does not exist, Pandas automatically initializes it with a structural schema; otherwise, it seamlessly appends the record without overwriting previous data.

​💡 Key Architectural Decisions

​Separation of Concerns: Core functionalities—such as API networking (requests), business logic/data manipulation (pandas), and terminal rendering—are entirely decoupled into dedicated, modular Python functions to ensure code maintainability.

​Security Compliance: By integrating a .env infrastructure, the project ensures that sensitive third-party API infrastructure tokens are completely isolated from version control tracking, adhering to standard DevOps security practices.
            KEY FEATURES

​Real-Time Data Ingestion: Establishes a live connection to the OpenWeatherMap REST API using the requests library to fetch up-to-the-minute global weather data.

​Robust JSON Parsing: Decodes complex, nested JSON payloads out of the box to isolate critical data points such as raw temperature, perceived ("feels like") temperature, humidity percentages, and wind velocity.

​Automated Pandas Data Pipeline: Utilizes a custom ETL (Extract, Transform, Load) workflow via Pandas that handles file creation and data mutation automatically—initializing the weather_history.csv database if missing, or appending rows without data fragmentation if it already exists.

​Polished CLI Dashboard: Renders data inside a structured, readable terminal user interface using visual separators and emoji indicators for a clean user experience.
 
​Production-Grade Secrets Management: Fully protects sensitive API infrastructure by decoupling credentials from the codebase using python-dotenv, ensuring private keys are never exposed to version control tracking.

​Defensive Error Handling: Employs explicit exception catch blocks to cleanly handle network drops, HTTP request bottlenecks, missing environment configurations, or invalid user-inputted city names without crashing the terminal.
 
       APPLICATION AND DATA FLOW 

This application follows a linear, modular pipeline architecture based on the ETL (Extract, Transform, Load) data processing pattern. It ensures a strict separation of concerns between user interaction, network communications, and disk I/O operations.

​High-Level Components

​User Interface (CLI Layer): Handles terminal input ingestion and final dashboard rendering.

​API Client (Extraction Layer): Constructs secure HTTP GET protocols and handles upstream payloads.

​Pandas Engine (Transformation & Loading Layer): Normalizes loose JSON primitives into rigid matrix vectors and handles local file mutations.


Step-by-Step Data Journey

​Extraction (API Fetching):
The program initializes and prompts the user for a targeted city. The fetch_weather_data function retrieves the underlying infrastructure key using python-dotenv and constructs a parameter payload containing the city name and targeted unit matrix (metric). It passes these values securely to the api.openweathermap.org endpoint via an asynchronous-blocking HTTP GET request.

​Transformation (JSON Parsing & Normalization):
Upon receiving a successful HTTP 200 OK status, the raw nested JSON payload is extracted. The save_to_history module intercepts this object and flattens out key key-value structures. Nestings such as main.temp and weather[0].description are isolated and transformed into native flat dictionary keys, mapped alongside an automated runtime execution Timestamp.

​Loading (Pandas Persistence):
The flattened dictionary is transformed instantly into a single-row structured Pandas DataFrame. The script runs a dynamic environmental file check on the host storage disk. If weather_history.csv is not present, Pandas acts as an initiator, compiling the document layout alongside its defined header strings. If it exists, it falls back to an append configuration (mode='a'), stacking the new data entry linearly to the bottom of the ledger.


 ​🛠️ 4. Tech Stack & Prerequisites


​This project is built using a highly dependable, data-centric Python stack designed to demonstrate efficient package handling, API interactions, and data storage.

​🖥️ Core Tech Stack

​Language: Python 3.8+ (Leverages native features like f-strings, dictionary .get() fault tolerances, and modular system packaging).

​API Ingestion: requests (v2.31.0+) – The industry standard HTTP client library for Python. Used to handle URL parameters, keep-alive connections, and raw response parsing safely.

​Data Engineering Engine: pandas (v2.2.0+) – A high-performance data manipulation and analysis library. Used in this pipeline to structurally map API fields, maintain the database schema, and commit row insertions safely to storage.

​Secrets Management: python-dotenv (v1.0.1+) – Parses key-value pairs from a separate .env file. Keeps infrastructure keys completely isolated out of source files to follow modern Twelve-Factor App security guidelines.

​📋 System Prerequisites

​Before spinning up the dashboard on your machine, ensure you have the following baseline environments configured 

Package Installer for Python (pip):
Ensure pip is installed alongside Python to fetch external repository libraries

OpenWeatherMap API Credentials:
To pull live conditions, you need a functional connection key:

​Navigate to the OpenWeatherMap Portal and register a free developer account.

​Head over to your dashboard profile menu under API Keys and generate a standard API endpoint token (it typically takes a few minutes to activate globally after generation).