# TRADIFY

![Tradify Logo](logo.svg)

**FIND. SWAP. OWN.**

WATCH THE [LIVE DEMO](https://drive.google.com/file/d/1WYpdlzQklEGmHKnVmEgBAV-eIM9pKB4c/view?usp=drive_link).

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Key Features](#2-key-features)
3. [System Architecture](#3-system-architecture)
4. [The AI Recommendation System](#4-the-ai-recommendation-system)
5. [Technology Stack](#5-technology-stack)
6. [Installation and Setup](#6-installation-and-setup)
7. [Team and Supervision](#7-team-and-supervision)

---

## 1. Project Overview

**Tradify** is a comprehensive e-commerce and community platform designed to promote sustainable consumption by facilitating the secure swapping, selling, renting, and donation of used products.

It addresses the lack of efficient, secure, and unified platforms for item exchange by integrating advanced features such as a personalized AI recommendation engine, robust user verification (including National ID for secure features), and rich community engagement tools (in-app chat, rating, user following, and private groups).

The system is developed with a **layered, modular architecture** to ensure high scalability, security, and maintainability across its primary components: a cross-platform mobile application and an administrative web panel.

## 2. Key Features

### Sustainable Exchange

* **Flexible Swapping:** Allows users to negotiate direct product swaps with or without predefined posts.
* **Multi-mode Listings:** Supports listing items for **Selling (Cash)**, **Swapping**, **Renting**, or **Donating**.
* **Diverse Categories:** Handles complex product types, including Automobiles, Real Estate, and Electronics, each with detailed, specific attribute fields.

### AI & User Experience

* **Personalized Recommendations:** Uses a **Neural Network-based Predictive Model** combined with a **Roulette Wheel Selection** mechanism to provide diverse and highly relevant product suggestions based on real-time user engagement metrics (comments, time spent, search history, favorites).
* **Seamless Onboarding:** Multiple authentication options (Email/Password, Google, Phone/OTP) with enhanced verification via National ID for secure transaction features.

### Community & Safety

* **Integrated Chat:** Secure, in-app messaging to facilitate direct negotiations between swappers and buyers.
* **User Following & Engagement:** Users can **follow** others to stay updated on new posts, fostering connections and community engagement.
* **Group Functionality:** Users can **create and join private groups** to organize niche communities around specific interests (e.g., specific car models or collectors).
* **Trust System:** Robust rating, review, and reporting mechanisms to ensure platform security and user credibility.

### Administrative Oversight

* **Robust Moderation:** Admin dashboard uses **Role-Based Access Control (RBAC)** to manage user accounts (block/warn/suspend), resolve reports, and approve posts.
* **Platform Statistics:** Displays real-time statistics on active users, opened/closed posts, and category usage for administrative monitoring.

## 3. System Architecture

Tradify employs a **layered architecture** built on modern cloud services, ensuring separation of concerns and independent component evolution (Figure 1: Architectural Diagram).

| Layer | Technology & Responsibility |
| :--- | :--- |
| **Front-end** | **Mobile App (Flutter):** Provides responsive, cross-platform user experience. **Admin Panel (React.js):** Tools for administration and content moderation. |
| **Back-end API** | **Spring Boot:** Core business logic, request handling, security (JWT, RBAC), and orchestration of services (Data, AI, Firebase). |
| **Data Layer** | **Firestore Database:** Scalable, document-based storage for user profiles, posts, and transactions. **Supabase Storage:** Stores media (images). |
| **AI Recommendation** | **Python (Flask API):** Serves the trained Neural Network model, handling prediction requests and roulette wheel calculation. |

## 4. The AI Recommendation System

The recommendation engine transitioned from traditional Collaborative Filtering to a specialized **Feedforward Neural Network (FNN)** functioning as a binary classifier.

### Methodology

The FNN predicts the probability (0 to 1) that a user will be interested in a specific product category.

* **Input Features:** Each user-category pair is represented by a 5-dimensional vector:

    1. `NumberOfComments`
    2. `TimeSpentOnCategoryInSec`
    3. `SearchOnCategory`
    4. `FavProductCategory`
    5. `InterestCategory` (Explicit/Implicit)

* **Post-Prediction Processing (Roulette Wheel Selection):** Probability scores are used as weights to proportionally distribute a fixed number of recommendation slots among the highly-rated categories. This ensures diversity while maintaining relevance.
* **API Integration:** The trained model is served via a lightweight **Flask API**, enabling seamless real-time prediction integration with the main Spring Boot backend.

## 5. Technology Stack

### Mobile Application (Flutter)

* **Framework:** Flutter, Dart
* **State Management:** Provider / BLOC Library
* **Design:** Material Design 3 Guidelines

### Backend and Core API

* **Framework:** Java 21, Spring Boot
* **Security:** Spring Security, JWT (Authentication), RBAC (Authorization), CORS configuration.
* **Integration:** Firebase Authentication, Google Maps Services.
* **Design:** MVC Pattern, DTOs for data transfer, Repository Pattern for data access abstraction.

### AI Service

* **Language:** Python
* **Serving:** Flask
* **ML Libraries:** TensorFlow, Keras, NumPy, Pandas (for data manipulation)

### Database and Infrastructure

* **Database:** Google Cloud Firestore (Primary NoSQL), Firebase Real-time Database (Synchronization).
* **Storage:** Supabase Storage (Media).

### Admin Web Panel

* **Framework:** React.js
* **Routing:** React Router

---

## 6. Installation and Setup

To run the Tradify platform locally, you must set up the three core components: the Backend API (Spring Boot), the AI Prediction Service (Flask), and your chosen Front-end (Mobile or Admin).

### Prerequisites

* Java Development Kit (JDK 21+)
* Maven
* Python (3.8+)
* Flutter SDK
* Node.js and npm/yarn (for React Admin Panel)
* Access to a Firebase Project (Auth, Firestore, Storage) configured with service account credentials.

### Step 1: Backend API Setup (Spring Boot)

1. Clone the repository:

    ```bash
    git clone https://github.com/Tradify-GP/backend
    cd tradify-backend
    ```

2. Configure `application-dev.properties` with your Firebase service account credentials and external API keys.
3. Build and run the Spring Boot application:

    ```bash
    ./mvnw spring-boot:run
    ```

    (The API will typically run on `http://localhost:8080`).

### Step 2: AI Prediction Service Setup (Flask)

1. Install Python dependencies:

    ```bash
    pip install -r requirements.txt # keras, flask, numpy, tensorflow, pandas
    ```

2. Ensure the trained model file (`trained_model.keras`) is in the Flask application directory.
3. Run the Flask application:

    ```bash
    python app.py
    ```

    (Ensure the Flask port is correctly referenced by the Spring Boot backend configuration).

### Step 3: Mobile Application Setup (Flutter)

1. Navigate to the mobile directory:

    ```bash
    cd tradify-mobile
    ```

2. Set up environment variables using `.env` file for API URLs.
3. Run the application on a connected device or emulator:

    ```bash
    flutter run
    ```

---

## 7. Team and Supervision

**Implemented by:**

| Student ID | Student Name | Role Emphasis |
| :--- | :--- | :--- |
| 20210032 | Ahmed Mohamed Shaaban | Admin Dashboard, Backend API, Firestore, AI Integration |
| 20210876 | Ali Mohammed Abduljabbar | Admin Dashboard |
| 20210605 | Badr Mohamed Ragab | Flutter Mobile App, Firebase Auth, Supabase Storage |
| 20211079 | Mohamed Amir Mohamed | Flutter Mobile App, Firebase Auth, Supabase Storage |
| 20210273 | Omar Mohamed Fayek | Backend API, Firestore |

**Supervised by:**

* **Dr. Basheer Youssef**
* **TA. Hassan Morad**

**Institution:** Cairo University, Faculty of Computers and Artificial Intelligence, Department of Computer Science.
