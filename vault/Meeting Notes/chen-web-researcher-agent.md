# Chen Web Researcher Agent

## Overview

חן היא סוכנת מחקר הרשת ב-AI Content OS — השלישית שנוספה לצוות אחרי יובל ויעל. תפקידה: לקבל בקשת חיפוש מראובן (נושא / מילות מפתח / סוג מאמר), לחפש ברשת באמצעות WebSearch + WebFetch, לסנן לפי קריטריוני איכות, ולשמור את הממצא כקובץ מוכן ב-`Content/YYYY-MM-DD-<slug>.md`. חן מנהלת זיכרון חיפושים ב-`chen/Memory/searches.md` — לפני כל חיפוש היא בודקת אם חיפשה משהו דומה ב-30 הימים האחרונים. חן לא מפעילה סוכנים אחרים; היא רק מכינה את הקרקע ומדווחת לראובן, שמחליט אם ומתי להפעיל את יעל לשכתוב.

## Open Questions

- יש לוודא שהפורמט של `chen/Memory/searches.md` עובד טוב עם Grep — האם כדאי להוסיף תגית `#search` לכל entry לזיהוי מהיר יותר?
- קריטריוני הסינון (✅/❌) הם כללי אצבע — ייתכן שיידרש calibration אחרי שימוש ראשון אמיתי.

## Session Log

### 2026-05-06 — הקמת סוכנת חן [shipped]

- **What was done:** הוקמה חן כ-subagent שלישי פעיל בצוות. נוצרו: `.claude/agents/chen.md` (הגדרת הסוכן עם tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep), `chen/agent.md` (pointer doc), `chen/Memory/searches.md` (stub לוג חיפושים). עודכן `reuven.md` — נוספה חן לטבלת הסוכנים (החלפת Agent 3 TBD), עודכן שורת Status, נוסף פרוטוקול "Chen → Yael Handoff" שמגדיר מתי ראובן ממשיך אוטומטית ליעל ומתי עוצר.
- **Decisions:** חן לא קוראת ישירות ליעל — רק ראובן מחליט. ההבחנה: אם הבקשה כללה כוונת שכתוב/פרסום → ראובן מפעיל יעל אוטומטית; אם הבקשה הייתה "מצא מאמר" בלבד → ראובן עוצר ומדווח. זיכרון ב-30 ימים: חיפוש דינמי (חדשות, מחירים) מתעלם מהזיכרון ותמיד מחפש מחדש.
- **Notes / Caveats:** `chen/Memory/searches.md` ריק — יתמלא בשימוש ראשון. tools מוגבלים במכוון: אין Bash, אין גישה ל-API חיצוני, אין Agent tool.
- **Related:** [[yael-content-writer-agent]], [[yuval-agent-gpt-image-gen]], [[ceo-agent-scaffold]]
