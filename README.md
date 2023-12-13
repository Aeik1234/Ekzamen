# Ekzamen
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Учет заявок на ремонт оборудования</title>
  <link rel="stylesheet" href="styles.css"> <!-- Подключаем внешний файл со стилями -->
</head>
<body>
  <h1>Учет заявок на ремонт оборудования</h1>

  <form id="addRequestForm"> <!-- Форма для добавления заявок -->
    <input type="text" id="requestNumber" placeholder="Номер заявки" required> <!-- Поле для номера заявки -->
    <input type="date" id="requestDate" required> <!-- Поле для даты заявки -->
    <textarea id="requestDescription" placeholder="Описание проблемы" required></textarea> <!-- Поле для описания проблемы -->
    <select id="requestStatus" required> <!-- Выпадающий список для выбора статуса заявки -->
      <option value="в ожидании">В ожидании</option>
      <option value="в работе">В работе</option>
      <option value="выполнено">Выполнено</option>
    </select>
    <button type="submit">Добавить заявку</button> <!-- Кнопка для отправки формы -->
  </form>

  <h2>Список заявок</h2>
  <ul id="requestList"></ul> <!-- Список для отображения заявок -->

  <h2>Список выполненных заявок</h2>
  <ul id="completedRequestList"></ul> <!-- Список для отображения выполненных заявок -->

  <script src="script.js"></script> <!-- Подключаем внешний файл со скриптом -->
</body>
</html>


// Код выполняется после загрузки всех элементов DOM
document.addEventListener('DOMContentLoaded', function() {
  // Получаем ссылки на необходимые элементы формы и списков
  const addRequestForm = document.getElementById('addRequestForm');
  const requestList = document.getElementById('requestList');
  const completedRequestList = document.getElementById('completedRequestList');

  // Добавляем обработчик события отправки формы
  addRequestForm.addEventListener('submit', function(event) {
    // Предотвращаем стандартное поведение отправки формы
    event.preventDefault();
    
    // Получаем значения полей формы
    const requestNumber = document.getElementById('requestNumber').value;
    const requestDate = document.getElementById('requestDate').value;
    const requestDescription = document.getElementById('requestDescription').value;
    const requestStatus = document.getElementById('requestStatus').value;

    // Создаем новый элемент списка и заполняем его данными из формы
    const newRequest = document.createElement('li');
    newRequest.innerHTML = `<strong>${requestNumber}</strong> - ${requestDescription} - ${requestStatus}`;
    
    // Проверяем статус запроса и добавляем элемент в соответствующий список
    if (requestStatus === 'выполнено') {
      newRequest.classList.add('completed'); // Добавляем класс "completed"
      completedRequestList.appendChild(newRequest); // Добавляем элемент в список выполненных запросов
    } else {
      requestList.appendChild(newRequest); // Добавляем элемент в основной список запросов
    }

    // Очищаем значения полей формы
    addRequestForm.reset();
  });
});

/* Стили для простого интерфейса */

/* Устанавливаем шрифт для всего документа */
body {
  font-family: Arial, sans-serif;
}

/* Устанавливаем отступ снизу для формы */
form {
  margin-bottom: 20px;
}

/* Устанавливаем отступ снизу и ширину для текстовых полей и селектора */
input, textarea, select {
  margin-bottom: 10px;
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

/* Устанавливаем отступы и стили для кнопок */
button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

/* Эффект при наведении на кнопку */
button:hover {
  background-color: #45a049;
}

/* Устанавливаем отступ сверху для заголовка второго уровня */
h2 {
  margin-top: 30px;
}

/* Убираем маркеры списка и отступы для элементов списка */
ul {
  list-style: none;
  padding: 0;
}

/* Устанавливаем отступы, границу и цвет фона для элементов списка с классом "completed" */
li.completed {
  margin-bottom: 10px;
  border: 1px solid #ccc;
  padding: 10px;
  background-color: #dff0d8;
}
