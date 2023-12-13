# Ekzamen
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Учет заявок на ремонт оборудования</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Учет заявок на ремонт оборудования</h1>

  <form id="addRequestForm">
    <input type="text" id="requestNumber" placeholder="Номер заявки" required>
    <input type="date" id="requestDate" required>
    <textarea id="requestDescription" placeholder="Описание проблемы" required></textarea>
    <select id="requestStatus" required>
      <option value="в ожидании">В ожидании</option>
      <option value="в работе">В работе</option>
      <option value="выполнено">Выполнено</option>
    </select>
    <button type="submit">Добавить заявку</button>
  </form>

  <h2>Список заявок</h2>
  <ul id="requestList"></ul>

  <h2>Список выполненных заявок</h2>
  <ul id="completedRequestList"></ul>

  <script src="script.js"></script>
</body>
</html>


document.addEventListener('DOMContentLoaded', function() {
  const addRequestForm = document.getElementById('addRequestForm');
  const requestList = document.getElementById('requestList');
  const completedRequestList = document.getElementById('completedRequestList');

  addRequestForm.addEventListener('submit', function(event) {
    event.preventDefault();
    const requestNumber = document.getElementById('requestNumber').value;
    const requestDate = document.getElementById('requestDate').value;
    const requestDescription = document.getElementById('requestDescription').value;
    const requestStatus = document.getElementById('requestStatus').value;

    const newRequest = document.createElement('li');
    newRequest.innerHTML = `<strong>${requestNumber}</strong> - ${requestDescription} - ${requestStatus}`;
    if (requestStatus === 'выполнено') {
      newRequest.classList.add('completed');
      completedRequestList.appendChild(newRequest);
    } else {
      requestList.appendChild(newRequest);
    }

    addRequestForm.reset();
  });
});

/* Стили для простого интерфейса */
body {
  font-family: Arial, sans-serif;
}

form {
  margin-bottom: 20px;
}

input, textarea, select {
  margin-bottom: 10px;
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

h2 {
  margin-top: 30px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  border: 1px solid #ccc;
  padding: 10px;
}

.completed {
  background-color: #dff0d8;
}
