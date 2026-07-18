# Read Order & Architecture Guide - Starter IL

## 1. ארכיטקטורת המערכת (High-Level Architecture)
המערכת נבנתה כ-Single Page Application (SPA) מבוססת React. 
בשלב ה-MVP הנוכחי, אנו מיישמים ארכיטקטורת **Mock Backend** (ללא שרת אמיתי), המשתמשת ב-React Context בשילוב `localStorage` כדי לסמלץ מסד נתונים חי (ניהול מלאי, הזמנות, וסשן משתמש). המטרה היא להוכיח לוגיקה עסקית (Business Logic) ויציבות Front-End לפני חיבור ל-Supabase/DB אמיתי.

## 2. סדר קריאת הקוד המומלץ (Recommended Reading Order)
כדי להבין את זרימת המידע במערכת, מומלץ לקרוא את הקוד לפי הסדר הבא:

1. **`src/context/AppContext.jsx` (מנוע הנתונים):**
   * זהו הלב של המערכת. כאן מוגדר ה-State הגלובלי שלנו.
   * מכיל את מערך המוצרים (`products`), סל הקניות (`cart`), היסטוריית ההזמנות (`orders`) וניהול ההרשאות המדומה (`user session`).

2. **`src/pages/Home.jsx` & `src/components/ProductCard.jsx`:**
   * כאן ניתן לראות את יישום הלוגיקה של המלאי בפרונט-אנד (תגיות "מלאי נמוך", או הצגת תמונה דהויה וחסימת כפתור רכישה כאשר `stock === 0`).

3. **`src/pages/Cart.jsx` & `src/pages/Checkout.jsx`:**
   * אזורי הרכישה. שימו לב לפונקציית הוולידציה שרצה לפני המעבר לקופה (Cart Validation), אשר מוודאת שכמות הפריטים בסל אינה חורגת מהמלאי העדכני ביותר ב-Context.

4. **`src/pages/AdminDashboard.jsx`:**
   * אזור הניהול. נגיש רק אם ה-Role של המשתמש הוא `admin`. מדגים יכולת עדכון מלאי (CRUD) בזמן אמת שמשפיעה מיד על חנות הלקוחות.

5. **`src/pages/QRInfoPage.jsx`:**
   * ראוט ציבורי (`/kit/:id`) שאינו דורש התחברות (No Auth). מדגים את הגישה השיווקית-ויראלית ומציג את פירוט התכולה לסריקה מהקופסה הפיזית.