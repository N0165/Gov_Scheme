Roshni — Renewable Energy Policy Explainer

Roshni is a browser-based renewable-energy policy explainer designed to help Indian citizens understand government renewable-energy schemes, subsidies, rooftop solar, solar pumps, net metering, and common application/fraud concerns.

The application provides two main experiences:

Get My Personalized Plan — a short questionnaire that uses the user's profile to generate a scheme-focused renewable-energy plan.

Ask Roshni Anything — a conversational interface for asking questions about the loaded renewable-energy information.

Important: Roshni is an informational assistant, not an official government source. Users are instructed to confirm final details with the official National Portal or their local DISCOM before applying.

Features

1. Personalized Renewable-Energy Plan

The plan flow asks users questions based on whether they are:

A homeowner interested in rooftop solar

A farmer interested in solar pumps or solar power generation

For homeowners, the questionnaire considers:

State

Average monthly electricity bill

Available sunlit roof area

Preferred method for covering upfront costs

For farmers, it considers:

State

Grid availability

Land size

Whether the user wants to sell surplus electricity

The generated plan is organized into:

Applies to You

Estimated Support

Your Next Steps

Sources

The application also provides options to start over, download the plan as a .txt file, or continue with a follow-up question.

2. Ask Roshni Anything

The chat interface allows users to:

Select suggested questions

Select topics from the sidebar

Type their own questions

Continue a conversation using previous chat context

The interface displays the answer together with the source used by Roshni when available.

3. Renewable-Energy Knowledge Base

The HTML file contains a built-in knowledge base covering five areas:

PM Surya Ghar — Muft Bijli Yojana

Information includes:

Rooftop solar for households

Central subsidy structure

Direct Benefit Transfer (DBT)

Free-electricity information

Collateral-free financing

Basic eligibility

Application process

Typical documents

ALMM requirements

Planning estimates for rooftop solar

PM-KUSUM

Information covers:

Component A — decentralized solar power plants and selling electricity to the DISCOM

Component B — standalone solar irrigation pumps

Component C — solarization of existing grid-connected agricultural pumps

Approximate subsidy and financing information

Farmer eligibility/use cases

Net Metering

The knowledge base explains:

Exporting surplus solar electricity to the grid

Importing electricity when solar generation is insufficient

Bi-directional metering

Net billing calculation

Central framework and state-level variation

Why users should confirm exact rules with their local DISCOM

Myths, FAQs & Practical Concerns

Examples include:

Solar generation during cloudy weather and winter

Whether rewiring is normally required

Solar maintenance

Grid-tied vs. off-grid systems

Whether solar automatically makes an electricity bill zero

Accessibility of solar for different household income levels

Avoiding Rejections & Fraud

The application provides guidance on:

Document mismatches

ALMM compliance

Property ownership proof

Bank-account details

Registered vendors

Official application channels

Fraud warning signs

Verifying information with the DISCOM or official portal

Multilingual Support

Roshni includes interface text for five languages:

English

हिंदी (Hindi)

தமிழ் (Tamil)

ਪੰਜਾਬੀ (Punjabi)

ગુજરાતી (Gujarati)

The page also switches the appropriate regional font when a language is selected.

Technology

The current application is implemented as a single HTML file containing:

HTML

CSS

Vanilla JavaScript

Embedded renewable-energy knowledge base

Client-side fallback logic

Anthropic API integration

Frontend

The interface uses:

Semantic HTML structure

CSS Grid and Flexbox

Responsive layout

Custom CSS variables

Google Fonts

Vanilla JavaScript for interactions

The design uses a warm paper-style background with teal, marigold, and brick accent colors.

AI Integration

The application contains a callClaude() function that sends requests to the Anthropic Messages API using the model specified in the source:

claude-sonnet-4-6

The AI is instructed to answer using only the application's embedded knowledge base.

The plan and chat prompts explicitly tell the model not to invent schemes, eligibility rules, or numbers that are not present in the knowledge base.

Fallback Mode

Roshni has client-side fallback behavior when the AI request does not return a usable response.

Personalized-plan fallback

The fallback calculates a rough rooftop-solar estimate using:

Monthly electricity bill

An assumed average tariff

Approximate generation of 120 units per kW per month

A rough system-size estimate

The subsidy rules stored in the knowledge base

Approximate savings and payback

For farmers, the fallback selects the relevant PM-KUSUM component based on grid access, land size, and interest in selling surplus electricity.

These calculations are explicitly presented as estimates rather than guarantees.

Chat fallback

If the live AI response is unavailable, the application performs a simple keyword-overlap search across the embedded knowledge base and returns the most relevant paragraph.

If no useful match is found, it tells the user that the information is not available in the current sources instead of guessing.

Application Flow

                    ┌──────────────────────┐
                    │       Roshni         │
                    │ Renewable Energy     │
                    │ Policy Explainer     │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        Personalized Plan              Ask Roshni
                 │                           │
                 ▼                           ▼
          User Questionnaire          User Question
                 │                           │
                 ▼                           ▼
          Citizen Profile              Chat Context
                 │                           │
                 └─────────────┬─────────────┘
                               ▼
                    ┌──────────────────────┐
                    │  Knowledge Base +    │
                    │  AI Instructions     │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴──────────┐
                    │                     │
                    ▼                     ▼
              Anthropic API          Local Fallback
                    │                     │
                    └──────────┬──────────┘
                               ▼
                    Personalized answer /
                    renewable-energy guidance

Project Structure

The current implementation is intentionally simple and contained in one HTML file:

Roshni/
└── index.html

The HTML file contains:

index.html
├── Page metadata
├── Google Font imports
├── CSS / responsive styling
├── Sidebar and topic navigation
├── Header and language selector
├── Personalized-plan tab
├── Chat tab
├── Embedded knowledge base
├── Multilingual UI strings
├── AI API integration
├── Personalized-plan logic
├── Chat fallback logic
├── Plan download functionality
└── Application initialization

Running the Project

Because the current project is a self-contained HTML page, it can be opened in a modern browser.

Option 1 — Open directly

Open the HTML file in a browser.

Option 2 — Run with a local web server

From the project directory, use any simple local HTTP server. For example, with Python:

python -m http.server 8000

Then open:

http://localhost:8000

API Configuration

The current implementation makes a browser-side request to:

https://api.anthropic.com/v1/messages

The source currently contains the API request logic directly in the HTML/JavaScript.

For a production deployment, the API integration should be moved behind a backend/server-side endpoint so that sensitive credentials are not exposed in client-side code.

A recommended production architecture would be:

Browser
   │
   ▼
Roshni Frontend
   │
   ▼
Backend API
   │
   ├── Knowledge / prompt handling
   │
   └── Anthropic API

Data and Source Handling

The application intentionally uses a constrained knowledge-base approach.

The AI prompts instruct Roshni to:

Use only the supplied knowledge base

Avoid inventing unsupported information

Clearly state when information is unavailable

Keep explanations simple

Remind users to verify final details with official authorities

The source data is marked in the application as last verified in September 2026.

Because renewable-energy schemes, subsidies, state regulations, tariffs, and application processes can change, the information should be re-checked before real-world use.

Security & Production Considerations

Before using Roshni as a public production application, consider:

Moving API calls to a backend

Keeping API credentials server-side

Adding authentication/rate limiting if required

Validating user input

Adding stronger source/version management

Keeping government-scheme information updated

Clearly separating estimates from official scheme values

Adding links to official government portals

Avoiding collection or storage of unnecessary personal information

Testing all multilingual content

Testing API failure, timeout, and offline behavior

Disclaimer

Roshni is designed as an informational and educational assistant. It does not replace official government portals, DISCOM guidance, or professional advice.

Users should verify current eligibility, subsidy amounts, documentation requirements, vendor registration, net-metering rules, financing terms, and application procedures with the relevant official authority before taking action.

Current Scope

Roshni currently focuses on:

Indian renewable-energy schemes

Rooftop solar

PM Surya Ghar

PM-KUSUM

Net metering

Solar adoption FAQs

Application rejection prevention

Fraud awareness

Personalized scheme guidance

It is not designed to provide unrestricted answers about every renewable-energy topic. When information is outside its loaded sources, its intended behavior is to say so rather than guess.
