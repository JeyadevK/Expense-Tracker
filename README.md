# Expense Tracker Application

## Features
- Track daily expenses with categories (Food, Transport, Entertainment)
- Set monthly budgets with alerts
- Generate spending reports
- Docker container support

## Setup

### Prerequisites
- Docker Desktop ([Download](https://www.docker.com/products/docker-desktop))
- Git (optional)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/expense-tracker.git
   cd expense-tracker

2. Build the Docker image:
  docker compose build



**Usage
Basic Commands**

# Add an expense
docker compose run --rm expense-tracker add-expense \
  --amount 15.50 \
  --category Food \
  --date 2025-04-10 \
  --description "Lunch"

# Set monthly budget
docker compose run --rm expense-tracker set-budget \
  --category Food \
  --month 4 \
  --year 2025 \
  --amount 500

# Generate monthly report
docker compose run --rm expense-tracker generate-report


Testing (Validates All Requirements)
Test 1: Basic Functionality

    1. Set a budget:
      docker compose run --rm expense-tracker set-budget --category Transport --month 4 --year 2025 --amount 300
    2. Add expenses until budget exceeded (should show alert)

Test 2: ORM Validation

    The system uses SQLAlchemy ORM (see models.py) with:

        Expense tracking table

        Budget constraints

        Date-based queries

Test 3: Edge Cases

    Try adding expense with invalid date

    Set duplicate budget for same category/month

    Generate report with no expenses

**Technical Implementation**

Database Schema

# models.py
class Expense(Base):
    __tablename__ = 'expenses'
    id = Column(Integer, primary_key=True)
    amount = Column(Float)
    category = Column(String)
    date = Column(Date)

class Budget(Base):
    __tablename__ = 'budgets'
    id = Column(Integer, primary_key=True)
    category = Column(String)
    month = Column(Integer)
    year = Column(Integer)
    amount = Column(Float)

Docker Configuration

# docker-compose.yml
services:
  expense-tracker:
    build: .
    volumes:
      - ./expenses.db:/app/expenses.db


## Troubleshooting

❌ "Docker not found"  
   - Install Docker Desktop and restart the terminal  

❌ "401 Unauthorized" when building  
   - Run `docker login` first  

