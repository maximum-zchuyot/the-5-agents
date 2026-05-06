# פוסט מזל שור

## Overview

פוסט תוכן בעברית על מזל שור (♉), מיועד לפייסבוק. הפוסט מדגיש תכונות מאפיינות של שור — סבלנות, נחישות, נאמנות ואהבה לנוחות — בטון רגשי עם קריאה לפעולה בתגובות. קובץ גלם שמור ב-`Content/2026-05-06-post-shor.md`. תמונה ויזואלית (שור בסגנון עדכני, ירוק/חום/זהב) יוצרה ע"י יובל ושמורה ב-`yuval/outputs/2026-05-06-shor-facebook.png`. הפוסט מוכן לבדיקה אחרונה לפני פרסום.

## Open Questions

- האם יש סגנון כתיבה מוגדר ב-`yael/style-guide.md` שצריך ליישר איתו לפני פרסום?

## Session Log

### 2026-05-06 — יצירת פוסט מזל שור [wip]

- **What was done:** נכתב פוסט גלם בעברית על מזל שור — טון רגשי, מבנה bullet + hook + CTA. נשמר ב-`Content/2026-05-06-post-shor.md`. כולל `{{IMAGE_NEEDED}}` placeholder לתמונה ויזואלית.
- **Decisions:** נכתב ישירות (ללא Chen) כי הבקשה הייתה יצירת תוכן מקורי, לא שכתוב מאמר קיים. סגנון "שור לא רץ — שור בונה" נבחר להדגשת הזהות האדמתית של המזל.
- **Notes / Caveats:** `yael/style-guide.md` עדיין placeholder — הפוסט טרם עבר שכתוב רשמי על ידי יעל. יש לאשר פלטפורמת יעד לפני שליחה.
- **Related:** [[yael-content-writer-agent]], [[yuval-agent-gpt-image-gen]]

### 2026-05-06 — ייצור תמונה + קיבוע פלטפורמה פייסבוק [wip]

- **What was done:** הופעל skill gpt-image-gen לייצור תמונה ויזואלית של שור (1024×1024, ירוק/חום/זהב, סמל ♉ משולב). התמונה נשמרה ב-`yuval/outputs/2026-05-06-shor-facebook.png`. עודכן קובץ התוכן — הוחלף `{{IMAGE_NEEDED}}` בנתיב התמונה, עודכנה פלטפורמה ל"פייסבוק".
- **Decisions:** השתמשנו ב-gpt-image-1 (לא gpt-image-2 שב-skill stub) כי gpt-image-2 לא קיים ב-API. מפתח OpenAI נמצא ב-.env עם ציטוטים — נוקו ב-PowerShell.
- **Notes / Caveats:** הפוסט עדיין לא עבר שכתוב רשמי ע"י יעל. style-guide ריק — יש לעדכן לפני שליחת יעל.
- **Related:** [[yuval-agent-gpt-image-gen]], [[yael-content-writer-agent]]

### 2026-05-06 — סנכרון לגיט [wip]

- **What was done:** כל ארבעת הקבצים של פוסט שור הועלו ל-git ו-pushed ל-origin/main: `Content/2026-05-06-post-shor.md`, `vault/Content Briefs/post-shor.md`, `yuval/outputs/2026-05-06-shor-facebook.png`, ועדכון `vault/Content Briefs/_index.md` (entry ראשון).
- **Decisions:** הסטטוס נשאר [wip] כי הפוסט עצמו עדיין לא פורסם — רק הסנכרון לרימוט בוצע. השלב הבא הוא שכתוב יעל + QA של גיא לפני פרסום אמיתי.
- **Notes / Caveats:** עכשיו שגיא חי, ה-pipeline המלא זמין — אבל הפוסט הנוכחי לא עבר עוד שכתוב יעל, ולכן גם לא הגיע לגיא. זה נשאר Open Question לסשן הבא.
- **Related:** [[guy-qa-agent]], [[yael-content-writer-agent]]
