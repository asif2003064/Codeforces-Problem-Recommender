# Codeforces Problem Recommender

A Django web application that recommends [Codeforces](https://codeforces.com/) competitive programming problems tailored to your skill level and weak areas.

## Features

- **Personalized Recommendations** — Enter your Codeforces handle and receive 6 problems matched to your rating and skill gaps.
- **Smart Grouping** — Users are automatically classified into skill groups (A–D) based on their current rating, each with curated topic sets and difficulty ranges.
- **Weakness Detection** — For users with 200+ submissions, the system identifies your top 3 struggled topics and factors them into recommendations.
- **Recent Problem Priority** — Recommendations prefer problems from recent contests so you practice on modern problem styles.
- **REST API** — Exposes API endpoints for integration with other tools or frontends.

## How It Works

| Your Rating  | Group | Problem Ratings     | Focus Topics                                           |
|-------------|-------|---------------------|--------------------------------------------------------|
| < 1000      | A     | 800 – 1000          | Brute force, implementation, math, strings, greedy     |
| 1000 – 1199 | B     | 1100 – 1400         | Binary search, graphs, trees, DFS, geometry            |
| 1200 – 1399 | C     | 1300 – 1600         | DP, combinatorics, number theory, DSU, shortest paths  |
| 1400+       | D     | 1500 – 1800         | All topics                                             |

## Tech Stack

- **Backend:** Python, Django 5.0, Django REST Framework
- **Frontend:** HTML, CSS, JavaScript (single-page template)
- **External API:** [Codeforces API](https://codeforces.com/apiHelp)
- **Database:** SQLite (default, currently unused)

## Getting Started

### Prerequisites

- Python 3.10+
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/asif-852/Codeforces-Problem-Recommender.git
cd Codeforces-Problem-Recommender

# Create a virtual environment
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run migrations
cd cf_recommender
python manage.py migrate

# Start the development server
python manage.py runserver
```

### Usage

1. Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.
2. Enter your Codeforces handle (e.g., `tourist`).
3. Click **Get Recommendations** to receive 6 personalized problems.

## API Endpoints

| Method | Endpoint                      | Description                                    |
|--------|-------------------------------|------------------------------------------------|
| GET    | `/`                           | Home page (HTML UI)                            |
| GET    | `/api/user/<handle>/`         | Returns Codeforces user profile info           |
| GET    | `/api/recommend/<handle>/`    | Returns recommended problems + topics          |

### Example Response (`/api/recommend/tourist/`)

```json
{
  "user_info": {
    "handle": "tourist",
    "rating": 3800,
    "rank": "legendary grandmaster",
    "group": "D"
  },
  "recommended_problems": [
    {
      "contestId": 1900,
      "index": "E",
      "name": "Example Problem",
      "rating": 1800,
      "tags": ["dp", "graphs"]
    }
  ],
  "important_topics": ["dp", "graphs", "..."],
  "struggle_topics": ["geometry", "fft"]
}
```

## Project Structure

```
Codeforces-Problem-Recommender/
├── cf_recommender/
│   ├── manage.py
│   ├── .env                          # Environment variables (not in git)
│   ├── config/                       # Django settings package
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── wsgi.py
│   │   └── asgi.py
│   └── codeforces_recommender/       # Main application
│       ├── views.py                  # API views & recommendation logic
│       ├── urls.py                   # URL routing
│       └── templates/
│           └── codeforces_recommender/
│               └── home.html         # Frontend UI
├── requirements.txt
├── README.md
└── .gitignore
```

## License

This project is open source. Feel free to use and modify it.
