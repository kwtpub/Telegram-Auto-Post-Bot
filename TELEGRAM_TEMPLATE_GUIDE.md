# Новый шаблон сообщений для Telegram

## Обзор

Создан специализированный шаблон для продажи китайских автомобилей в формате **"только онлайн"** без возможности живого просмотра.

## 🚗 Особенности нового шаблона

### ✅ Преимущества формата
- **Четкая структура** с эмодзи для удобства чтения
- **Фокус на онлайн-продаже** с явными указаниями
- **Уникальные ID** в формате XXX-XXX (например, `023-455`)
- **Системные хештеги** для поиска и категоризации
- **Оптимальная длина** до 1024 символов для Telegram

### 🔥 Ключевые элементы
- **Пометка "ТОЛЬКО ОНЛАЙН"** в цене
- **Блок предупреждений** о формате продажи
- **Акцент на китайских брендах** и их преимуществах
- **Связь только через Telegram** (без номеров телефонов)
- **Доставка по РФ** и безналичный расчет

## 📋 Структура сообщения

```
🚗 **[МАРКА МОДЕЛЬ]** • [ГОД] • [ПРОБЕГ] км

💰 **[ЦЕНА] руб.** • 🔥 **ТОЛЬКО ОНЛАЙН**

🔧 **Характеристики:**
• Двигатель: [ДАННЫЕ]
• КПП: [ТИП]
• Привод: [ТИП]
• Комплектация: [НАЗВАНИЕ]
• Цвет: [ЦВЕТ]

⚡ **Что включено:**
• [КЛЮЧЕВЫЕ ОПЦИИ]
• Официальная гарантия до 5 лет
• Сервисная книжка в наличии

🛡️ **Состояние:**
• [ОПИСАНИЕ СОСТОЯНИЯ]
• Все документы в порядке
• Готов к передаче

⚠️ **ВАЖНО - ОНЛАЙН ПРОДАЖА:**
🚫 Живой просмотр недоступен
💬 Связь только в Telegram
📦 Доставка по РФ возможна
💳 Безналичный расчет

📋 **ID автомобиля:** `[XXX-XXX]`

#китайскиеавто #онлайнпродажа #[марка][модель] #[город]
```

## 💻 Использование в коде

### Базовое использование

```python
from app.utils.message_formatter import MessageFormatter

# Подготовка данных
car_data = {
    'brand': 'Geely',
    'model': 'Atlas Pro',
    'year': '2023',
    'mileage': '45000',
    'price': '2850000',
    'engine': '2.0л, 190 л.с., бензин',
    'transmission': 'автомат CVT',
    'drive_type': 'передний',
    'trim': 'Luxury',
    'color': 'белый перламутр',
    'condition': 'отличное состояние',
    'custom_id': '023-455',
    'city': 'Москва'
}

# Форматирование
formatter = MessageFormatter()
message = formatter.format_for_telegram(car_data)
```

### Прямое использование шаблона

```python
from app.utils.message_formatter import TelegramMessageTemplate
from app.utils.id_generator import generate_custom_id

message = TelegramMessageTemplate.format_chinese_car_online_sale(
    brand="BYD",
    model="Song Plus",
    year="2024",
    mileage="25000",
    price="3500000",
    engine="1.5л турбо + электромотор, 218 л.с.",
    transmission="автомат e-CVT",
    drive_type="полный",
    trim="GL-i",
    color="синий металлик",
    condition="идеальное состояние",
    custom_id=generate_custom_id(),
    additional_features=[
        "адаптивная подвеска", 
        "автопилот 2 уровня", 
        "беспроводная зарядка"
    ],
    city="Новосибирск"
)
```

## 🔧 Интеграция с Perplexity API

Обновлен промпт для генерации объявлений с учетом онлайн-формата:

```python
from app.perplexity_api.text_formatter import CarInfo, create_car_description_prompt

# Создание объекта с данными автомобиля
car_info = CarInfo(
    brand="Chery",
    model="Tiggo 7 Pro Max",
    year="2024",
    price="3200000",
    custom_id="394-954"
    # ... остальные поля
)

# Генерация промпта для онлайн-продажи
prompt = create_car_description_prompt(
    car_info, 
    custom_context="Дополнительная информация об автомобиле"
)
```

## 📊 Тестирование и валидация

### Проверка длины сообщения

```python
from app.utils.message_formatter import TelegramMessageTemplate

# Проверка валидности длины
is_valid = TelegramMessageTemplate.validate_message_length(message, 1024)
print(f"Валидная длина: {'Да' if is_valid else 'Нет'}")
```

### Извлечение хештегов

```python
# Получение списка хештегов
hashtags = TelegramMessageTemplate.extract_hashtags(message)
print(f"Хештеги: {', '.join(hashtags)}")
```

## 🏷️ Система хештегов

### Обязательные хештеги
- `#китайскиеавто` - общий тег для китайских авто
- `#онлайнпродажа` - указание на формат продажи
- `#[марка][модель]` - уникальный тег автомобиля (без пробелов)
- `#[город]` - город продажи в нижнем регистре

### Примеры хештегов
- `#geelyatlaspro` для Geely Atlas Pro
- `#cherytiggo7promax` для Chery Tiggo 7 Pro Max
- `#havaljolion` для Haval Jolion
- `#bydsongplus` для BYD Song Plus

## 🎯 Результаты тестирования

✅ **Все тесты пройдены успешно:**
- Длина сообщений: 690-714 символов (в пределах лимита 1024)
- Валидность формата: 100%
- Хештеги генерируются корректно
- Custom ID в формате XXX-XXX работает

## 📈 Преимущества нового подхода

1. **Четкая коммуникация** - покупатель сразу понимает формат продажи
2. **Доверие** - детальная информация о гарантии и документах
3. **Удобство поиска** - системные хештеги и уникальные ID
4. **Экономия времени** - нет лишних вопросов о возможности просмотра
5. **Масштабируемость** - шаблон легко адаптируется под разные модели

## 🔄 Интеграция в процесс

Новый шаблон полностью интегрирован в:
- `app/utils/announcement_processor.py` - основной процессор объявлений
- `app/utils/message_formatter.py` - форматирование сообщений
- `app/perplexity_api/text_formatter.py` - промпты для AI
- `app/utils/id_generator.py` - генерация уникальных ID

---

*Документация актуальна на дату создания. При изменениях в коде обновляйте соответствующие разделы.* 