# Техническое задание: Rail-X Telegram Mini App
## Маркетплейс одежды без складов

### 📱 Концепция проекта

**Rail-X** - революционный маркетплейс одежды в формате Telegram Mini App, работающий без складов с прямой курьерской доставкой от продавцов к покупателям за 2-10 часов.

### 🎯 Ключевые преимущества Telegram формата

- **Мгновенный доступ**: Без установки отдельного приложения
- **Встроенные уведомления**: Через Telegram
- **Интеграция с платежами**: Telegram Payments
- **Социальные функции**: Шаринг, отзывы, каналы
- **Геолокация**: Автоматическое определение района для курьеров

## 🎨 Дизайн-система

### Цветовая палитра
```
Основной фон: #1e1e1e (матовый черный)
Акцентный цвет: #64DDA0 (фирменный мятный)
Текст основной: #ffffff (белый)
Текст вторичный: #b0b0b0 (серый)
Фон карточек: #2a2a2a (темно-серый)
Границы: #3a3a3a (средне-серый)
Ошибки: #ff4757 (красный)
Успех: #64DDA0 (мятный)
```

### Типографика
```
Заголовки: SF Pro Display, 24-32px, bold
Подзаголовки: SF Pro Display, 18-20px, medium  
Основной текст: SF Pro Text, 14-16px, regular
Мелкий текст: SF Pro Text, 12px, regular
Цены: SF Pro Display, 18-24px, bold, мятный цвет
```

### UI Компоненты
- **Кнопки**: Скругленные углы 12px, мятный градиент
- **Карточки**: Скругленные углы 16px, тень 0 4px 12px rgba(0,0,0,0.3)
- **Инпуты**: Темный фон, мятная обводка при фокусе
- **Иконки**: Outline стиль, 24px, мятный цвет

## 🔧 Техническая архитектура

### Frontend (Telegram WebApp)
```
Framework: React 18 + TypeScript
State: Zustand / Redux Toolkit
Styling: Styled-components / Emotion
UI Kit: Custom компоненты + Telegram UI
Build: Vite / Webpack 5
PWA: Service Worker для кеширования
```

### Telegram Integration
```javascript
// Инициализация Telegram WebApp
window.Telegram.WebApp.ready();
window.Telegram.WebApp.expand();

// Кнопка "Назад" в шапке Telegram
window.Telegram.WebApp.BackButton.show();

// Основная кнопка для покупок
window.Telegram.WebApp.MainButton.setText('Купить за 2 490 ₽');
window.Telegram.WebApp.MainButton.show();

// Haptic feedback
window.Telegram.WebApp.HapticFeedback.impactOccurred('medium');

// Геолокация
window.Telegram.WebApp.LocationManager.getLocation();
```

### Backend API
```
Node.js + Express / NestJS
Database: PostgreSQL + Redis
File Storage: AWS S3 / Yandex Object Storage
Payments: Telegram Payments + ЮKassa
Auth: Telegram Login Widget
Real-time: WebSockets / Server-Sent Events
```

## 📱 Пользовательские сценарии

### 1. Первый запуск
```
1. Пользователь нажимает на бота/ссылку → Telegram Mini App
2. Автоматическая авторизация через Telegram
3. Запрос геолокации для определения района доставки
4. Онбординг: 3 экрана с основными преимуществами
5. Переход в каталог
```

### 2. Просмотр каталога
```
1. Главный экран: категории одежды + поиск
2. Фильтры: размер, цена, бренд, время доставки
3. Карточки товаров: фото, цена, время доставки
4. Быстрый просмотр: свайп по фото
5. Добавление в избранное одним тапом
```

### 3. Покупка товара
```
1. Страница товара: галерея, описание, отзывы
2. Выбор размера + проверка наличия у продавцов
3. Расчет времени доставки по районам
4. Добавление в корзину / Быстрая покупка
5. Checkout через Telegram Payments
6. Отслеживание курьера в реальном времени
```

### 4. Продавец
```
1. Регистрация через отдельного бота
2. Загрузка товаров: фото + описание + цена
3. Управление остатками
4. Уведомления о новых заказах
5. Интерфейс вызова курьера
6. Статистика и аналитика
```

## 🎯 MVP Функционал

### Покупатель
- [x] Авторизация через Telegram
- [x] Каталог с фильтрами
- [x] Корзина и избранное  
- [x] Оформление заказа
- [x] Telegram Payments
- [x] Отслеживание доставки
- [x] История заказов
- [x] Отзывы и рейтинги

### Продавец (отдельный бот)
- [x] Регистрация и верификация
- [x] Добавление товаров
- [x] Управление остатками
- [x] Получение заказов
- [x] Интерфейс курьера
- [x] Аналитика продаж

### Курьер (отдельный бот)
- [x] Регистрация курьера
- [x] Получение заказов
- [x] Навигация к продавцу/покупателю
- [x] Подтверждение выдачи
- [x] Статистика доходов

## 🖼️ Структура экранов

### Главное меню (Bottom Navigation)
```
🏠 Главная    🔍 Поиск    ❤️ Избранное    🛒 Корзина    👤 Профиль
```

### Экраны приложения

#### 1. Главная
```
- Баннер с акциями
- Быстрые категории (Мужское, Женское, Аксессуары)
- "Быстрая доставка" (товары с доставкой <3 часов)
- Рекомендации
- Новинки
```

#### 2. Каталог/Поиск  
```
- Строка поиска с автокомплитом
- Фильтры (выдвижная панель)
- Сортировка (цена, время доставки, рейтинг)
- Сетка товаров 2x2 / список
- Бесконечная прокрутка
```

#### 3. Карточка товара
```
- Галерея фото (свайп + зум)
- Название, бренд, артикул
- Цена с учетом доставки
- Выбор размера (с таблицей размеров)
- Время доставки по районам
- Описание + характеристики
- Отзывы с фото
- Похожие товары
- Кнопки: "В корзину" / "Купить сейчас"
```

#### 4. Корзина
```
- Список товаров с миниатюрами
- Изменение количества/размера
- Промокоды и скидки
- Расчет доставки
- Итоговая сумма
- Кнопка "Оформить заказ"
```

#### 5. Оформление заказа
```
- Адрес доставки (автозаполнение по геолокации)
- Выбор времени доставки
- Способ оплаты (Telegram Payments)
- Комментарий к заказу
- Подтверждение заказа
```

#### 6. Отслеживание
```
- Статус заказа (принят, собирается, в пути, доставлен)
- Карта с курьером в реальном времени
- Контакты курьера (звонок/чат)
- Estimated time of arrival
```

#### 7. Профиль
```
- Аватар и имя из Telegram
- История заказов
- Избранное
- Адреса доставки
- Настройки уведомлений
- Поддержка
```

## 🔔 Push-уведомления через Telegram

### Для покупателей
```
- Заказ принят в обработку
- Курьер выехал к продавцу
- Курьер забрал товар и едет к вам
- Курьер прибыл (за 5 минут)
- Заказ доставлен
- Просьба оставить отзыв
```

### Для продавцов  
```
- Новый заказ
- Курьер едет за товаром
- Курьер прибыл за товаром
- Товар передан курьеру
- Еженедельная статистика продаж
```

### Для курьеров
```
- Новый заказ в вашем районе
- Навигация к продавцу
- Навигация к покупателю  
- Еженедельная статистика доходов
```

## 💰 Интеграция платежей

### Telegram Payments
```javascript
// Инициация платежа
window.Telegram.WebApp.openInvoice(invoice_url);

// Обработка результата
window.Telegram.WebApp.onEvent('invoiceClosed', (data) => {
  if (data.status === 'paid') {
    // Заказ оплачен
    redirectToOrderTracking(data.slug);
  }
});
```

### Поддерживаемые методы
- 🏦 Банковские карты (Visa, MasterCard, МИР)
- 💳 Apple Pay / Google Pay  
- 🏧 SberPay / ЮMoney
- 📱 Оплата через Telegram Stars

## 📍 Геолокация и районирование

### Определение района доставки
```javascript
// Получение геолокации
const location = await window.Telegram.WebApp.requestLocation();

// Определение района Москвы
const district = await API.getDeliveryDistrict(location.latitude, location.longitude);

// Расчет времени доставки
const deliveryTime = await API.calculateDeliveryTime(district, sellersLocations);
```

### Покрытие MVP (Москва)
```
Приоритетные районы:
- ЦАО (центр)
- САО (север) 
- СВАО (северо-восток)
- ВАО (восток)
- ЮВАО (юго-восток)

Время доставки: 2-10 часов
Зоны покрытия: в пределах МКАД + ближнее Подмосковье
```

## 🚀 Roadmap разработки

### Фаза 1 (MVP) - 2 месяца
```
✅ Telegram Mini App setup
✅ Базовый UI Kit (черный + мятный)
✅ Каталог товаров
✅ Корзина и оформление заказа
✅ Telegram Payments
✅ Простое отслеживание
✅ Боты для продавцов и курьеров
```

### Фаза 2 - 1 месяц  
```
🔄 Продвинутые фильтры
🔄 Персональные рекомендации
🔄 Live-трекинг курьеров
🔄 Система отзывов с фото
🔄 Программа лояльности
🔄 Уведомления в реальном времени
```

### Фаза 3 - 1 месяц
```
🔄 AR примерка (виртуальная)
🔄 Видео-отзывы  
🔄 Социальные функции (шаринг образов)
🔄 Telegram каналы брендов
🔄 Интеграция с Telegram Stories
🔄 Голосовой поиск
```

## 🔒 Безопасность и конфиденциальность

### Данные пользователей
- Минимальный набор: только из Telegram профиля
- Адреса доставки: шифрование в БД
- Платежи: PCI DSS через провайдеров
- GDPR compliance для пользователей из ЕС

### Telegram Integration Security
```javascript
// Валидация данных от Telegram
function validateTelegramData(data) {
  const secret = crypto.createHash('sha256')
    .update(BOT_TOKEN)
    .digest();
    
  const hmac = crypto.createHmac('sha256', secret)
    .update(data)
    .digest('hex');
    
  return hmac === receivedHash;
}
```

## 📊 Аналитика и метрики

### KPI для MVP
```
👥 DAU/MAU пользователей
🛒 Conversion rate (просмотр → покупка)
⏱️ Среднее время доставки
💰 Средний чек
⭐ Рейтинг товаров и доставки
🔄 Retention rate (возвраты пользователей)
```

### Telegram Analytics
```javascript
// Трекинг событий через Telegram
window.Telegram.WebApp.sendData(JSON.stringify({
  event: 'purchase_completed',
  order_id: orderId,
  amount: totalAmount,
  delivery_time: deliveryTimeHours
}));
```

## 🎯 Конкурентные преимущества в Telegram

1. **Мгновенный доступ**: Без установки приложения
2. **Встроенная вирусность**: Легкий шаринг в чатах
3. **Push без разрешений**: Уведомления через Telegram
4. **Глобальный охват**: 800М+ пользователей Telegram
5. **Низкие барьеры входа**: Знакомый интерфейс
6. **Интеграция с экосистемой**: каналы, боты, платежи

## 💻 Техническая спецификация

### Требования к устройствам
```
iOS: 10.0+ (Safari WebView)
Android: 5.0+ (Chrome WebView)  
Desktop: Telegram Desktop / Web
Интернет: 3G+ для основного функционала
Offline: Кеширование каталога на 24 часа
```

### Performance
```
🚀 Первая загрузка: <2 секунд
⚡ Переходы между экранами: <300ms
📱 Размер бандла: <500KB gzip
🔄 API Response time: <500ms
📷 Lazy loading изображений
💾 Progressive Web App с offline кешем
```

### API Endpoints
```
GET /api/v1/products - каталог товаров
GET /api/v1/product/:id - детали товара  
POST /api/v1/cart - добавление в корзину
POST /api/v1/order - создание заказа
GET /api/v1/order/:id/track - отслеживание
POST /api/v1/payment/telegram - Telegram Payments webhook
```

## 🎨 UI/UX Гайдлайны

### Принципы дизайна
1. **Telegram-native**: Соответствие гайдлайнам Telegram
2. **Thumb-friendly**: Удобство для одной руки
3. **Темная тема**: Экономия батареи + премиум вид
4. **Минимализм**: Фокус на товарах
5. **Быстродействие**: Мгновенные отклики

### Адаптивность
```
Mobile Portrait: 375-428px (primary)
Mobile Landscape: 667-926px  
Tablet: 768-1024px
Desktop: 1200px+ (через Telegram Desktop)
```

### Анимации
```css
/* Фирменные переходы */
.transition-fast { transition: all 0.15s ease-out; }
.transition-normal { transition: all 0.3s ease-out; }
.transition-slow { transition: all 0.5s ease-out; }

/* Hover эффекты (только desktop) */
@media (hover: hover) {
  .card:hover { transform: translateY(-4px); }
}

/* Мятный градиент для кнопок */
.btn-primary {
  background: linear-gradient(135deg, #64DDA0 0%, #4ECDC4 100%);
}
```

Это полноценное техническое задание для создания Rail-X маркетплейса в формате Telegram Mini App. Хочешь, чтобы я детализировал какие-то конкретные разделы или добавил дополнительные технические спецификации? 