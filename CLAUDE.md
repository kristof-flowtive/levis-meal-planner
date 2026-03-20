# Claude.md

## Project Overview
Build a simple online dashboard for weekly meal planning for an 8.5 month old baby boy following a Baby Led Weaning approach.

The dashboard is for the user's wife to use easily on a phone or laptop.

The core purpose is:
- View the full upcoming week at once
- Plan 2 meals per day: breakfast and lunch
- Generate a grocery list for the upcoming week
- Always show the grocery list for next week on Sunday
- Keep the interface extremely simple, clean, and fast to use

---

## Product Requirements

### Main Features
1. **Weekly Meal Planner**
   - Show all 7 days of the week in one view
   - Each day should have:
     - Breakfast
     - Lunch
   - Meals should be editable
   - Meals should persist after refresh

2. **Sunday Grocery List**
   - On Sundays, prominently show the grocery list for the next week
   - Grocery list should be automatically generated from all meals planned for the upcoming week
   - Combine duplicate ingredients into one list item where possible

3. **Simple Dashboard UX**
   - Minimal design
   - Mobile-friendly first
   - Easy for a non-technical user
   - Fast editing with as few clicks as possible

4. **Meal + Ingredient Structure**
   - Each meal should support:
     - Meal name
     - Ingredients list
     - Optional notes
   - Grocery list should be derived from ingredients used across the week

---

## Suggested MVP Scope
Start with a very basic MVP before adding complexity.

### MVP should include:
- Weekly grid with Monday to Sunday
- 2 meal slots per day:
  - Breakfast
  - Lunch
- Ability to type in meal names manually
- Ability to attach ingredient lists to each meal
- Auto-generated grocery list
- Sunday grocery list highlight
- Local persistence using browser storage or a very lightweight backend

### Do NOT include yet unless needed later:
- Authentication
- Complex nutrition tracking
- Recipe scraping
- AI meal recommendations
- Multi-user collaboration
- Shopping delivery integrations

Keep the MVP small and working first.

---

## Recommended Tech Stack
Use a lightweight stack that Claude Code can build quickly.

### Preferred
- **Frontend:** React + Next.js
- **Styling:** Tailwind CSS
- **State / Persistence:** localStorage first, then optionally Supabase later
- **Deployment:** Vercel

### Why
- Quick to build
- Easy to iterate
- Easy to deploy
- Good mobile responsiveness
- Minimal infrastructure required

---

## Functional Rules

### Week View
- Display a 7-day week view
- Default to the current week
- Allow moving to next week and previous week
- Each day contains:
  - Breakfast card
  - Lunch card

### Grocery List Logic
- Grocery list should be generated from the selected/planned meals for the next week
- If today is Sunday, the grocery list for the upcoming week should be shown prominently at the top
- Ingredient duplicates should be merged where sensible
  - Example:
    - "banana"
    - "bananas"
    - should ideally become one item if normalization is implemented
- If exact quantity logic is too complex for MVP, start with a de-duplicated ingredient checklist

### Data Persistence
- Meal entries should persist between sessions
- Use localStorage for MVP unless otherwise specified
- Data structure should be clean enough to upgrade later to a database

---

## UX Requirements
Design for a busy parent.

### UI principles
- Extremely clear layout
- Large tap targets
- Minimal clutter
- Neutral, pleasant colours
- Clear separation by day
- Grocery list should be printable or easy to screenshot

### Ideal layout
- Header with week range
- Weekly planner grid
- Grocery list section
- Sunday banner or callout when grocery prep is relevant

---

## Data Model
Use simple structured objects.

### Example
```ts
type Meal = {
  name: string;
  ingredients: string[];
  notes?: string;
};

type DayPlan = {
  breakfast: Meal | null;
  lunch: Meal | null;
};

type WeekPlan = {
  weekStart: string; // ISO date
  days: {
    monday: DayPlan;
    tuesday: DayPlan;
    wednesday: DayPlan;
    thursday: DayPlan;
    friday: DayPlan;
    saturday: DayPlan;
    sunday: DayPlan;
  };
};
```
