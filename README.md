# APPS-releases

מאגר שחרורים לאפליקציות של Tomas — קבצי APK ומטא-נתוני גרסאות בלבד.
הקוד עצמו יושב בריפואים פרטיים נפרדים.

## מבנה

כל אפליקציה בתת-תיקייה משלה:

```
agrotom/
├── version.json              # פרטי הגרסה העדכנית
├── AgroTom-x.y.z.apk         # קובץ ההתקנה של הגרסה העדכנית
└── archive/                  # גרסאות ישנות (אופציונלי)
```

האפליקציה עצמה קוראת את `version.json` דרך URL של raw:

```
https://raw.githubusercontent.com/tomas1983-arch/APPS-releases/main/<app>/version.json
```

## נוהל שחרור גרסה חדשה

1. בונים APK חדש
2. מעבירים את ה-APK הישן ל-`archive/` (אופציונלי, אך שומר גיבוי)
3. מעלים את ה-APK החדש לתיקיית האפליקציה
4. מעדכנים את `version.json` — `version`, `versionCode`, `apkUrl`, `notes`, `releaseDate`
5. Commit ו-push

**חשוב:** `versionCode` חייב לעלות בכל release, אחרת אנדרואיד לא יאפשר התקנה מעל גרסה קיימת.

## פורמט version.json

| שדה | חובה | מטרה |
|-----|-----|------|
| `version` | ✓ | מחרוזת גרסה למשתמש (למשל `"2.9.5"`) |
| `versionCode` | ✓ | מספר רץ, זהה ל-`versionCode` ב-build.gradle |
| `apkUrl` | ✓ | קישור הורדה ישיר ל-APK |
| `minSupportedVersion` |   | אם תרצה יום אחד לחייב עדכון במקום להציע |
| `releaseDate` |   | פורמט `YYYY-MM-DD` |
| `notes` |   | תיאור השינויים, מוצג בדיאלוג העדכון |

## אפליקציות

- **agrotom** — מוניטור לחות קרקע מבוסס ESP32 ואפליקציית אנדרואיד לצפייה בגרפים
