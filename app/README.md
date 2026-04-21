PZ 1.4 - Виконання додатку Adroid

**Спойлер: залупа ебаное ебал все що там є**

Цей документ описує процес створення Android-застосунку "TestApp", включаючи налаштування середовища, проектування інтерфейсу користувача та програмування логіки взаємодії.
1. Налаштування проєкту та середовища
1.1 Створення проєкту

    Запуск: Запустіть Android Studio через термінал командою studio.

    Тип проєкту: Оберіть New Project -> Phone and Tablet -> Basic Views Activity.

    Конфігурація:

        Name: TestApp (має починатися з великої літери).

        Language: Kotlin.

        Minimum SDK: API 34 ("UpsideDownCake"; Android 14.0).

    Завершення: Натисніть Finish і зачекайте завершення синхронізації Gradle ( Gradle sync finished).

1.2 Налаштування емулятора

    Відкрийте Tools > Device Manager.

    Натисніть Create Device і оберіть профіль Pixel 6a.

    У вкладці x86 Images оберіть системний образ UpsideDownCake (Google APIs).

    Назвіть пристрій Pixel 6a API 34 і натисніть Finish.

    Запустіть емулятор натисканням кнопки Play.

2. Проектування інтерфейсу користувача (UI)

Робота ведеться у файлі res/layout/content_main.xml у режимі Design.
2.1 Ресурси рядків (strings.xml)

Для підтримки чистоти коду всі текстові значення винесені у файл res/values/strings.xml:

    Hello -> "Hello World!" 

    MessageString -> "Hello!" 

2.2 Компоненти екрана

На макет додано наступні віджети через панель Palette:
Віджет	ID	Властивості	Опис
TextView	MessageLabel	Text: @string/MessageString, Size: 24sp, Alignment: center	

Виводить привітання
EditText	MessageText	Hint: "Please Enter Your Name.", Width: match_constraint	

Поле для вводу імені
Button	ShowButton	Text: "Display Your Message"	

Запускає логіку привітання
2.3 Обмеження (Constraints)

Після розміщення кожного елемента необхідно використовувати інструмент Infer Constraints (іконка чарівної палички), щоб зафіксувати їх положення на екрані.
3. Програмування логіки (MainActivity.kt)

Логіка застосунку реалізована мовою Kotlin у файлі MainActivity.kt.
3.1 Оголошення змінних

У класі MainActivity оголошено змінні для доступу до UI-компонентів:
Kotlin

var mMessageLabel: TextView? = null
var mMessageText: EditText? = null
var mShowButton: Button? = null

(Примітка: Використовуйте Alt+Enter для імпорту класів TextView, EditText та Button) .
3.2 Зв'язування View та обробка подій

У методі onCreate після setContentView виконується ініціалізація та налаштування обробника натискання:
Kotlin

// 1. Отримання посилань на об'єкти за їх ID
mMessageLabel = findViewById<View>(R.id.MessageLabel) as TextView
mMessageText = findViewById<View>(R.id.MessageText) as EditText
mShowButton = findViewById<View>(R.id.ShowButton) as Button

// 2. Встановлення обробника подій для кнопки
mShowButton!!.setOnClickListener {
    // Формування повідомлення на основі вводу користувача
    val msg = "Hello, " + mMessageText!!.text.toString()
    // Виведення тексту в мітку
    mMessageLabel!!.text = msg
}
