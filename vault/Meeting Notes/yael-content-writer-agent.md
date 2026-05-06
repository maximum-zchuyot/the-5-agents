# Yael Content Writer Agent

## Overview

יעל היא סוכנת כתיבת תוכן ב-AI Content OS — השנייה שנוספה לצוות אחרי יובל. תפקידה: לקבל מאמר גלם מ-`Content/`, לשכתב אותו בסגנון הכתיבה שלנו (לפי `yael/style-guide.md` + דוגמאות ב-`yael/reference/`), ולהחזיר לראובן פלט מוכן. כשיעל מזהה שתמונה תחזק את המאמר, היא מכניסה `{{IMAGE_NEEDED: "..."}}` placeholder — ראובן הוא שמפעיל את יובל ומחליף את ה-placeholders בתמונות אמיתיות. יעל מוגבלת לכלים Read/Write/Edit/Glob/Grep בלבד, ואינה יכולה להפעיל סוכנים אחרים.

## Open Questions

- `yael/style-guide.md` הוא placeholder בלבד — יש למלא אותו לפני שמשתמשים ביעל בפועל
- `yael/reference/` ריקה — יש להוסיף דוגמאות לטקסטים בסגנון שלנו

## Session Log

### 2026-05-06 — הקמת סוכנת יעל [shipped]

- **What was done:** הוקמה יעל כ-subagent שני פעיל בצוות. נוצרו: `.claude/agents/yael.md` (הגדרת הסוכן), `yael/agent.md` (pointer doc), `yael/style-guide.md` (placeholder), `yael/reference/.gitkeep`, `Content/`, `Content/Ready/`, `Output/`. עודכן `reuven.md` — נוספה יעל לטבלת הסוכנים + פרוטוקול IMAGE_NEEDED לאינטגרציה עם יובל.
- **Decisions:** יעל מעבדת מאמר אחד בלבד לכל הפעלה (ראובן מציין filename ספציפי). "העברה" של הקובץ המקורי מתבצעת דרך Write+overwrite stub בלבד (ללא Bash/mv) כי יעל מוגבלת לכלים ללא Bash. פרוטוקול IMAGE_NEEDED נשאר בבעלות ראובן — יעל רק מסמנת, יובל מייצר, ראובן מחבר.
- **Notes / Caveats:** style-guide.md ו-reference/ ריקים — יעל לא תייצר פלט איכותי עד שימולאו. הטמעת `tools:` ב-frontmatter של yael.md כדי לאכוף הגבלת כלים.
- **Related:** [[yuval-agent-gpt-image-gen]], [[ceo-agent-scaffold]]
