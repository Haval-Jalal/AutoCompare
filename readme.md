# AutoCompare

A .NET 9 console application that evaluates whether a car is worth buying. Enter a license plate number and receive a recommendation based on mileage history, ownership count, insurance claims, and known model issues.

---

## Recommendation System

Each search returns one of three verdicts:

| Rating | Meaning |
|---|---|
| **Good buy** | Low mileage, few owners, no serious flags |
| **Ok buy** | Acceptable condition with some warning signs |
| **Not a good buy** | High risk — many owners, crashes, failed inspection, or known model problems |

---

## What the App Analyzes

- **Mileage** — aggregates history and calculates average mileage per year
- **Number of owners** — how many times the car has changed hands
- **Insurance claims** — crashes and repairs (dummy data, prepared for API)
- **Inspection records** — passed / failed / remarks
- **Known model issues** — internal database linked to make and model
- **AI analysis** — GPT-4o-mini for deeper questions about the car or model

---

## Tech Stack

| Component | Technology |
|---|---|
| Language & runtime | C# / .NET 9 (Console App) |
| Console UI | Spectre.Console — tables, colors, menus |
| Data persistence | JSON files (users.json, cars.json, logs.json) |
| AI | OpenAI GPT-4o-mini via HTTP |
| SMS verification | Twilio Verify |
| Email verification | SMTP over Gmail |
| Configuration | DotNetEnv (`.env`) + .NET User Secrets |
| Password security | SHA-256 hashing |
| Authentication | Two-factor — email or SMS |

---

## Project Structure

```
AutoCompare/
├── Program.cs          # Entry point — initializes DataStore and runs UIManager
├── UIManager.cs        # All menu logic and user flows
├── CarSearch.cs        # Car lookup, scoring, and table display
├── Car.cs              # Car model + Recommendation enum (GoodInvestment, Acceptable, RiskyPurchase)
├── User.cs             # User model with search history (List<string>)
├── DataStore.cs        # Generic JSON persistence — loads and saves any List<T>
├── AIService.cs        # High-level wrapper for AI calls
├── AiHelper.cs         # Low-level OpenAI chat completions client
├── TwoFactor.cs        # Two-factor verification via email (SMTP) and SMS (Twilio)
├── Admin.cs            # Admin panel
├── Logger.cs           # Static logging to logs.json
└── Config.cs           # Reads and validates environment variables from .env
```

---

## Configuration

Create a `.env` file in the project root:

```env
SMTP_EMAIL=your@gmail.com
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_PASSWORD=your-app-password

TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxx
TWILIO_AUTH_TOKEN=xxxxxxxxxxxxxxxx
TWILIO_PHONE_NUMBER=+1xxxxxxxxxx
TWILIO_VERIFY_SERVICE_SID=VAxxxxxxxxxxxxxxxx

OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
```

Sensitive values can also be stored via .NET User Secrets:

```bash
dotnet user-secrets set "OPENAI_API_KEY" "sk-..."
```

---

## Getting Started

**Requirements:** .NET 9 SDK

```bash
git clone https://github.com/pauline8712/AutoCompare.git
cd AutoCompare
dotnet run
```
