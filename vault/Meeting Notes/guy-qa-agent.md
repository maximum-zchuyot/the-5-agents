# Guy QA Agent

## Overview

גיא הוא סוכן ה-Quality Assurance הרביעי והאחרון בצוות AI Content OS — סוגר הלולאה לפני שתוצר מגיע למשתמש. תפקידו: לקבל מראובן path לתוצר סופי + הבריף המקורי + מספר סבב, לרוץ על צ'קליסט QA מובנה (רלוונטיות, סגנון, שלמות, תמונות, תקינות טכנית), ולהפיק דוח ב-`guy/QA_Reports/<YYYY-MM-DD-HHMM>-<slug>.md`. גיא הוא הסוכן היחיד שמורשה לדחות תוצר. הוא מוגבל לכלים Read/Glob/Grep/Write בלבד — אין לו Edit על התוצר, אין Bash, אין Web. ראובן מנהל את לולאת התיקונים: אם גיא דוחה, ראובן מפעיל את יעל מחדש עם ההערות; סבב 3 הוא התקרה — אז ראובן מציג למשתמש להחלטה ידנית.

## Open Questions

- האם הצ'קליסט (5 קטגוריות) מספק לכל סוגי התוצרים, או שצריך וריאנט לסוגי תוכן שונים (פוסט קצר vs מאמר ארוך vs newsletter)?
- מה קורה אם `yael/style-guide.md` עדיין placeholder — האם גיא מסמן warning או דוחה את התוצר?
- שמירת ההיסטוריה ב-`guy/QA_Reports/` תצמח עם הזמן — האם נצטרך indexing/retention policy?

## Session Log

### 2026-05-06 — הקמת סוכן גיא [shipped]

- **What was done:** הוקם גיא כ-subagent רביעי וסוגר הצוות. נוצרו: `.claude/agents/guy.md` (הגדרה קנונית, frontmatter אנגלית + system prompt עברית עם 6 שלבי workflow וצ'קליסט 5 קטגוריות, tools: Read/Glob/Grep/Write בלבד), `guy/agent.md` (pointer doc עברית), `guy/QA_Reports/.gitkeep`. עודכן `reuven.md` — גיא החליף את "Agent 4 [TBD]" בטבלת ה-Sub-Agents, נוסף סקשן חדש "QA Loop Protocol" שמגדיר את לולאת התיקונים (עד 3 סבבים, escalation ידני בסבב 3), עודכנה שורת Status להצהיר "the team is complete" עם השרשרת המלאה, נוספה הערה ב-Quality Review Checklist שמפנה לגיא לתוצרי תוכן.
- **Decisions:** **גיא לא יכול לעשות Edit על התוצר** — אכיפה ארכיטקטונית דרך מגבלת tools ב-frontmatter. רק יעל יכולה לערוך פלט; גיא רק קורא ומדווח. **תקרת 3 סבבים** — מנגנון בטיחות נגד לולאות אינסופיות; בסבב 3 ראובן מעביר את ההחלטה למשתמש ולא מנסה סבב 4. **גיא ממלא את slot 4** ולא נוסף כשורה חמישית — שומר על המבנה המקורי של ה-PRD (4 sub-agents) ותואם לקריאת המשתמש "הסוכן ה-5 והאחרון בשרשרת" כשסופרים את ראובן + 4 הכפיפים. **כלל הכרעה בצ'קליסט:** כשל בקטגוריות 4א-4ג (רלוונטיות/סגנון/מבנה) → דחייה אוטומטית; כשל ב-4ד-4ה (תמונות/טכני) → תלוי חומרה.
- **Notes / Caveats:** גיא לא יכול להחזיר ישירות ליעל בגלל מגבלת ארכיטקטורה של Claude Code (sub-agent לא מפעיל sub-agent אחר) — כל ה-routing דרך ראובן, וזה תועד מפורשות גם ב-system prompt של גיא וגם ב-pointer doc וגם ב-reuven.md. הצ'קליסט עצמו תופס מקום מרכזי ב-system prompt — אם נרצה לשנות אותו, השינוי יהיה בקובץ אחד. `guy/QA_Reports/` יתחיל ריק (.gitkeep בלבד) ויתמלא בשימוש ראשון.
- **Related:** [[yael-content-writer-agent]], [[yuval-agent-gpt-image-gen]], [[chen-web-researcher-agent]], [[ceo-agent-scaffold]]
